# Utilities and Helpers

ACA Engine comes packaged with some handy helper functions that make interfacing with the wide variety of common IoT protocols  easier.

## Functions and Constants

These can be included into your driver class

```ruby
include ::Orchestrator::Constants
```

| Helper | Type | Description |
| :--- | :--- | :--- |
| `On, Down, Open` | true | Constants that can make code more readable |
| `Off, Up, Close, Short` | false | Constants that can make code more readable |
| `in_range(input_number, max, min = 0)` | returns a number in the range | if input exceeds the limits, the limit is returned |
| `is_affirmative? value` | returns true if value is affirmative | values such as: `true 'yes' :On` |
| `is_negatory? value` | returns true if value is negative | values such as: `false 'no' :Inactive` |

The Constants include module also contains Configuration Helpers

```ruby
include ::Orchestrator::Transcoder
```

| Helper | Type | Description |
| :--- | :--- | :--- |
| `hex_to_byte(data)` | returns binary string | accepts any string containing hex characters and supports common formatting such as `"0xDEADBEEF"`, `"De:ad:Be:ef"` etc |
| `byte_to_hex(data)` | returns an ASCII string | accepts binary strings or arrays of bytes |
| `str_to_array(data)` | returns an array of bytes | accepts strings |
| `array_to_str(data)` | returns a binary string | accepts array of bytes |

## Protocols

### WebSockets

Enables [WebSocket communication](https://en.wikipedia.org/wiki/WebSocket) using a standard TCP socket driver.

* For more details on the websocket API see [https://github.com/faye/websocket-driver-ruby\#driver-api](https://github.com/faye/websocket-driver-ruby#driver-api)

```ruby
require 'protocols/websocket'class WebsocketClient    include ::Orchestrator::Constants    include ::Orchestrator::Transcoder    generic_name :Websocket    descriptive_name 'Websocket example'    tcp_port 80    wait_response false    def connected        new_websocket_client    end    def disconnected        # clear the keepalive ping        schedule.clear    end    # Send a text message    def some_request        @ws.text "hello"        # or json format etc        @ws.text({            some: "message",            count: 234        }.to_json)    end    # send a binary message    def binary_send        @ws.binary("binstring".bytes)        # or        @ws.binary hex_to_byte("0xdeadbeef")    end    protected    def new_websocket_client        # NOTE:: you must use wss:// when using port 443 (TLS connection)        @ws = Protocols::Websocket.new(self, "ws://#{remote_address}/path/to/ws/endpoint")        # @ws.add_extension # https://github.com/faye/websocket-extensions-ruby        # @ws.set_header(name, value) # Sets a custom header to be sent as part of the handshake        @ws.start    end    def received(data, resolve, command)        @ws.parse(data)        :success    end    # ====================    # Websocket callbacks:    # ====================    # websocket ready    def on_open        logger.debug { "Websocket connected" }        schedule.every('30s') do            @ws.ping('keepalive')        end    end    def on_message(raw_string)        logger.debug { "received: #{raw_string}" }        # Process request here        # request = JSON.parse(raw_string)        # ...    end    def on_ping(payload)        logger.debug { "received ping: #{payload}" }        # optional    end    def on_pong(payload)        logger.debug { "received pong: #{payload}" }        # optional    end    # connection is closing    def on_close(event)        logger.debug { "closing... #{event.code} #{event.reason}" }    end    # connection is closing    def on_error(error)        logger.debug { "ERROR! #{error.message}" }    end    # ====================end
```

### Telnet

Implements the [telnet standard](https://en.wikipedia.org/wiki/Telnet) so that it is easy to communicate with devices that implement control codes or require negotiation.

```ruby
require 'protocols/telnet'class TelnetClient    def on_load        new_telnet_client        # Telnet client returns only relevant data for buffering        config before_buffering: proc { |data|            @telnet.buffer data        }    end    def disconnected        # Ensures the buffer is cleared        new_telnet_client    end    def some_request        # Telnet deals with end of line characters        # (may have been negotiated on initial connection)        send @telnet.prepare('some request')    end    protected    def new_telnet_client        # Telnet client needs access to IO stream        @telnet = Protocols::Telnet.new do |data|            send data        end    endend
```

### KNX

Constructs [KNX standard](https://en.wikipedia.org/wiki/KNX_%28standard%29) datagrams that make it easy to communicate with devices on KNX networks.

For more information see: [https://github.com/acaprojects/ruby-knx](https://github.com/acaprojects/ruby-knx)

### BACnet

Constructs [BACnet](http://www.bacnet.org/) datagrams that make it easy to communicate with devices on BACnet networks.

For more information see: [https://github.com/acaprojects/ruby-bacnet](https://github.com/acaprojects/ruby-bacnet)

### OAuth

For secure delegated access to services that implement it see [wikipedia for details](https://en.wikipedia.org/wiki/OAuth)

```ruby
require 'protocols/oauth'class HttpClient    # =====================================    # Hook into HTTP request via middleware    # All requests will be sent with OAuth    # =====================================    def on_update        connected    end    # This is called directly after on_load.    # Middleware is not available until connected    def connected        @oauth = Protocols::OAuth.new({            key:    setting(:consumer_key),            secret: setting(:consumer_secret),            site:   remote_address        })        update_middleware    end    protected    def update_middleware        # middleware is service helper function        mid = middleware        mid.clear        mid << @oauth    endend
```

### SNMP

Provides an evented IO proxy for [ruby-netsnmp](https://github.com/swisscom/ruby-netsnmp)

```ruby
require 'protocols/snmp'class SnmpClient    include ::Orchestrator::Constants    udp_port 161    def on_unload        @client.close    end    # This is called directly after on_load.    # Middleware is not available until connected    def connected        proxy = Protocols::Snmp.new(self)        @client = NETSNMP::Client.new({            proxy: proxy, version: "2c",            community: "public"        })    end    def query_something        self[:status] = @client.get(oid: '1.3.6.1.2.1.1.1.0')    end    def set_something(val)        @client.set('1.3.6.1.2.1.1.3.0', value: val)        self[:something] = val    end    protected    def received(data, resolve, command)        # return the data which resolves the request promise.        # the proxy uses fibers to provide this to the NETSNMP client        data    endend
```

### SOAP Services

Probably the easiest way to use these services at the moment via a Logic module. There are a number of supported ruby gems:

* [https://github.com/savonrb/savon](https://github.com/savonrb/savon)
* [https://github.com/unwire/handsoap](https://github.com/unwire/handsoap)

#### **Savon usage:**

```ruby
# Ensure we are not blocking the IO reactor looprequire 'httpi/adapter/libuv'require 'savon'HTTPI.adapter = :libuv# Make requests as per the savon documentationclient = Savon.client(wsdl: 'https://aca.im/service.wsdl')logger.debug { "Available operations: #{client.operations}" }
```

#### **Handsoap usage:**

```ruby
# Ensure we are not blocking the IO reactor looprequire 'handsoap/http/drivers/libuv_driver'Handsoap.http_driver = :libuv# Make requests as per the handsoap documentation
```

### Wake on LAN

Wake on LAN is available to drivers of all types

```ruby
# Supports any string with the correct number of hex digits#  as well as common formats (these are some examples)mac_address_string = '0x62f81d4b6f00'mac_address_string = '62:f8:1d:4b:6f:00'mac_address_string = '62-f8-1d-4b-6f-00'# Defaults to broadcast address `'255.255.255.255'`wake_device(mac_address_string)# You can define a VLan gateway for a directed broadcast (most common in enterprise)wake_device(mac_address_string, '192.168.3.1')
```

### ICMP \(ping\)

Uses the operating systems `ping` utility to perform a connectivity check.

```ruby
# perform the pingping = ::UV::Ping.new(remote_address)ping.ping      # true / false to indicate success / failure# check out the ping resultsping.pingable  # true / false to indicate success / failureping.ip        # IP pinged (remote_address can be a domain name)ping.exception # any error messagesping.warning   # any warning messages
```

### CRC Checks

[github project](https://github.com/dearblue/ruby-crc) and [supported CRC checks](https://github.com/dearblue/ruby-crc/blob/master/lib/crc/_modules.rb)

* `gem install crc`

Usage

```ruby
require 'crc'crc = CRC::CRC16_CCITT.newcrc.update "\x12\x34\x56\x78\x90"crc.digest # => "ca"
```


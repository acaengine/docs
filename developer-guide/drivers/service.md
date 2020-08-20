# Service Drivers

Service drivers interface with devices that communicate using the HTTP\(S\) protocol. Currently HTTP versions 1.0 and 1.1 are supported.

They are similar to Device Drivers with two major differences:

1. It’s not recommended to use the common `received` function
2. They do not have a `send` function

This is because HTTP is much more contextual than many protocols. It’ll often only return success whereas many custom device protocol responses can be interpreted without knowledge of the original request.

## Sending a Request

Each request should either set the `on_receive` callback option or provide a block for response processing.

| Method | Arguments | Description |
| :--- | :--- | :--- |
| request | verb, path, options = {}, &blk | allows you to pass in a custom verb |
| get | path, options = {}, &blk |  |
| post | path, options = {}, &blk |  |
| put | path, options = {}, &blk |  |
| delete | path, options = {}, &blk |  |

```ruby
# Example usage:

def query_position
    # Get request will look like:
    # http://domain.or.ip/api/status_of?coordinates=detailed
    get('/api/status_of', {
        query: {
            coordinates: :detailed
        }
    }) do |data, resolve, command|
        check_response(data) do |resp|
            # Update status (made available to interfaces)
            self[:position] = resp['coords']
        end
    end
end

def check_response(data)
    # Check response status
    # (might have been 500 or 404, depends on what you are expecting)
    if data.status == 200
        begin
            # We're assuming a JSON response and we are passing that data
            # back to the calling function and assuming success at this point
            yield ::JSON.parse(data.body) if block_given?
            return :success
        rescue => e
            logger.print_error e
        end 
    end

    # Fail if there are any issues
    # Obviously this behaviour depends on the service etc
    :abort
end
```

### Request Options

<table>
  <thead>
    <tr>
      <th style="text-align:left">Option</th>
      <th style="text-align:left">Example</th>
      <th style="text-align:left">Effect</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left"><code>query</code>
      </td>
      <td style="text-align:left"><code>query: &quot;me=bob&amp;other=rain&quot;</code> or
        <br /> <code>query: {<br />  me: :bob,<br />  other: :rain<br />}</code>
      </td>
      <td style="text-align:left">URI<b>?me=bob&amp;other=rain</b>
      </td>
    </tr>
    <tr>
      <td style="text-align:left"><code>body</code>
      </td>
      <td style="text-align:left"><code>body: &quot;data=hello&amp;other=world&quot;</code> or
        <br /> <code>body: {<br />  data: :hello,<br />  other: :world<br />}</code>
      </td>
      <td style="text-align:left">when body is a string it will be sent as is. When a hash, it will be form
        encoded.</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>headers</code>
      </td>
      <td style="text-align:left">
        <p><code>headers: {<br />  Name: &apos;value&apos;</code>
        </p>
        <p><code>}</code>
        </p>
      </td>
      <td style="text-align:left">Some headers are transformed further. See bellow</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>file</code>
      </td>
      <td style="text-align:left"><code>file: &apos;path/to/file.ext&apos;</code>
      </td>
      <td style="text-align:left">Will send the file as the body</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>keepalive</code>
      </td>
      <td style="text-align:left"><code>keepalive: false</code>
      </td>
      <td style="text-align:left">Will close the connection once the request has completed</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>ntlm</code>
      </td>
      <td style="text-align:left"><code>ntlm: {<br />  user: &apos;u&apos;,<br />  password: &apos;p&apos;,<br />  domain: &apos;d&apos;<br />}</code>
      </td>
      <td style="text-align:left">Will perform a request with an endpoint that requires NTLM auth</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>digest</code>
      </td>
      <td style="text-align:left"><code>digest: {<br />  user: &apos;u&apos;,<br />  password: &apos;p&apos;,<br />  domain: &apos;d&apos;<br />}</code>
      </td>
      <td style="text-align:left">Will perform a request with an endpoint that requires digest auth</td>
    </tr>
    <tr>
      <td style="text-align:left"><code>proxy</code>
      </td>
      <td style="text-align:left"><code>proxy: {<br />  host: &apos;1.2.3.4&apos;,<br />  port: 80,<br />  username: &apos;bob&apos;,<br />  password: &apos;hunter2&apos;<br />}</code>
      </td>
      <td style="text-align:left">Use a proxy server for the request.</td>
    </tr>
  </tbody>
</table>

NOTE:: Both NTLM and Digest auth are challenge response protocols and won’t work with HTTP 1.0 or keep alive false

### Basic Authentication

Basic auth is supported natively along with NTLM and digest authentication techniques. All that is required is to set the `authorization` header like so:

```ruby
options = {
    headers: {
        authorization: [username, password]
    }
}
```

For more advanced methods of authentication see Utilities and Helpers.

## Handling a Response

The response object is passed to your received block and looks like this:

```ruby
get '/' do |data|
    # Response body as a string
    data.body

    # HTTP version the server is using (a string)
    data.http_version

    # The status code returned as an integer
    data.status

    # Was the connection kept alive for possible further requests
    data.keep_alive

    # What cookies have been stored at this path (as a Hash)
    data.cookies
    data.cookies['user_id']

    # The data object itself is a hash of all the headers
    data['Content-Type'] # => 'text/html'
end
```

## Cookies

Cookies are handled in the background in the same way a browser would handle cookies.

There is a helper method that can be used to clear cookies: `clear_cookies`

You can set cookies by setting the `cookie` header field. Supports both strings and hashes.

## Proxy Support

When building drivers that need to communicate with external endpoints, its good practice to provide proxy support. This can be achieved by passing the `proxy` parameter with requests. To provide user support of these, these can be loaded from settings and set as part of the defaults for every request.

```ruby
def on_update
    proxy = setting(:proxy)
    if proxy
        config({
            proxy: {
                host: proxy[:host],
                port: proxy[:port]
            }
        })
    end
end
```


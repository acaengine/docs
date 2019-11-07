# debug

This lowers the drivers log level to debug and forwards messages to the connection.

```javascript
{    "id": 4,    "cmd": "debug",    "sys": "sys-Z6XXA-Kc_v",    "mod": "Bookings",    "index": 1,    "name": "debug"}
```

Responds with the module ID that uniquely identifies the code being monitored

```javascript
{    "id": 4,    "type": "success",    "mod_id": "mod-Z6XXB1doL4",    "meta": {        "sys": "sys-Z6XXA-Kc_v",        "mod": "Bookings",        "index": 1    }}
```

Log messages are then sent to the browser

```javascript
{    "type": "debug",    "mod": "mod-Z6XXB1doL4",    "klass": "::Some::Display",    "level": "debug",    "msg": "input changed to HDMI"}
```


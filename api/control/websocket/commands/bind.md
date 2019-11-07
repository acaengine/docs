# bind

The `bind` command is used to subscribe module state changes on the current connection. When creating the binding, the current state will be returned immediately.

Bindings are ephemeral, being discarded when the connection is closed.

```javascript
{
    "id": 1,                 // tracking id, to pair request and response
    "cmd": "bind",           // request type
    "sys": "sys-OEtOZqd_2J", // the system containing the target
    "mod": "Display",        // module name
    "index": 1,              // module index in the system
    "name": "power"          // status variable you are interested in
}
```

A typical response to the above request:

```javascript
{
    "id": 1,                  // tracking id
    "type": "success",        // request status (success or error)
    "meta": {                 // meta data that might be useful
        "sys": "sys-YNQ8uNfJvF",
        "mod": "Display",
        "index": 1,
        "name": "power"
    }
}
```

Once an active binding is in place, the server will push value changes.

```javascript
{
    "type": "notify",
    "value": true,
    "meta": {
        "sys": "sys-YNQ8uNfJvF",
        "mod": "Display",
        "index": 1,
        "name": "power"
    }
}
```


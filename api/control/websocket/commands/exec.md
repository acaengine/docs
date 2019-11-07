# exec

The `exec` command performs an action on a module within the system. It is a remote procedure call.

```javascript
{    "id": 3,                 // tracking id    "cmd": "exec",           // request type    "sys": "sys-YNQ8ucvndO", // system id    "mod": "Display",        // module name    "index": 2,              // module index in the system    "name": "switch_to",     // the driver function to call    "args": ["hdmi"]         // The function arguments (if required)}
```

The return value of the function is returned in the response, assuming it can be serialised into JSON.

```javascript
{    "id": 3,    "type": "success",    "value": ["hdmi"]}
```

If an error was raised, the error message is returned.

```javascript
{    "id": 3,    "type": "error",    "code": 3,    "msg": "ZeroDivisionError: divided by 0"}
```


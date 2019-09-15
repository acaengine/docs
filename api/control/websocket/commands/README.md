# Commands

Command messages are the basis for interacting with the real-time API. All commands take the form of a JSON payload, and will return a JSON response.

| Attribute | Type | Description |
| :--- | :--- | :--- |
| `id` | number or string | A unique ID to associated with the command. This is returned as part of the response. Generally an incrementing counter, however any string or numerical value may be used. |
| `cmd` | string | The command type. One of `bind`, `unbind`, `exec`, `debug`, or`ignore`. |
| `sys` | string | The system ID that the command targets. |
| `mod` | string | The name of the module that the command targets. |
| `name` | string |  |


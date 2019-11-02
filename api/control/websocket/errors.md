# Errors



| Name | Code | Description |
| :--- | :--- | :--- |
| parse error | `0` | invalid JSON sent to the server |
| bad request | `1` | request was missing required fields |
| access denied | `2` | you don’t have permission to access this system, the access attempt is logged |
| request failed | `3` | an error was raised or a promise rejected when processing the request |
| unknown command | `4` | the command type unknown, the connection is logged as suspicious |
| system not found | `5` | the system does not exist |
| module not found | `6` | the module does not exist in the system |
| unexpected failure | `7` | a framework level error occurred \(this should never happen\) |


# Systems

The `/systems` endpoint provides methods for discovering, creating and interacting with systems. For more on the role that systems play, see:

{% page-ref page="../../key-concepts/systems.md" %}

All systems provide a base set of metadata that helps to describe their role and capabilities, as well as provide references to the modules they contain, and the zones they exist in.

## Model

| Attribute | Type | Description |
| :--- | :--- | :--- |
| id | `string` | The system's unique ID. |
| edge\_id | `string` | ID of the preferred engine node to run on. |
| name | `string` | The system's primary identifier. |
| zones | `array` | Zone IDs that this system is a member of. |
| modules | `array` | Module ID's that this system contains. |
| description | `string` | Markdown formatted text that describes the system. |
| email | `string` | Calendar email that represents this system. Typically used for room scheduling / bookings. |
| capacity | `integer` | Number of people this space can accommodate. |
| features | `string` | List of features in the room for searching and filtering spaces. |
| bookable | `boolean` | Flag for signifying the space is bookable. |
| installed\_ui\_devices | `integer` | Expected number of fixed installation touch panels. |
| settings | `object` | JSON object representing the system's configuration. |
| created\_at | `integer` | Timestamp of creation. |
| support\_url | `string` | A URL linking to the primary interface for controlling this system. |
| version | `integer` | Incremental counter for handling stale updates. |

## Discovery

{% api-method method="get" host="https://example.com" path="/api/control/systems" %}
{% api-method-summary %}
Search
{% endapi-method-summary %}

{% api-method-description %}
Direct queries to the systems endpoint list, or search for existing systems.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="q" type="string" required=false %}
A search query for the system metadata.
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
Max results to return \(default 20\).
{% endapi-method-parameter %}

{% api-method-parameter name="offset" type="integer" required=false %}
The offset within the result set.
{% endapi-method-parameter %}

{% api-method-parameter name="zone\_id" type="string" required=false %}
Limit to systems within this zone.
{% endapi-method-parameter %}

{% api-method-parameter name="module\_id" type="string" required=false %}
Limit to systems that contain this module.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
A list of systems matching the search criteria.
{% endapi-method-response-example-description %}

```javascript
{
    "total": 3,
    "results": [
        {
            "edge_id": "edge-QC03B3OM",
            "name": "Room 1",
            "description": null,
            "email": "room1@example.com",
            "capacity": 10,
            "features": "",
            "bookable": true,
            "installed_ui_devices": 0,
            "zones": [
                "zone-rGhCRp_aUD"
            ],
            "modules": [
                "mod-rJRCVYKVuB",
                "mod-rJRGK21pya",
                "mod-rJRHYsZExU"
            ],
            "settings": {},
            "created_at": 1562041110,
            "support_url": null,
            "version": 5,
            "id": "sys-rJQQlR4Cn7"
        },
        {
            "edge_id": "edge-QC03B3OM",
            "name": "Room 2",
            "description": null,
            "email": "room2@example.com",
            "capacity": 10,
            "features": "",
            "bookable": true,
            "installed_ui_devices": 0,
            "zones": [
                "zone-rGhCRp_aUD"
            ],
            "modules": [
                "mod-rJRJOM27Kb",
                "mod-rJRLE4_PQ7",
                "mod-rJRLwe72Mo"
            ],
            "settings": {},
            "created_at": 1562041127,
            "support_url": null,
            "version": 4,
            "id": "sys-rJQSySsELE"
        },
        {
            "edge_id": "edge-QC03B3OM",
            "name": "Room 3",
            "description": null,
            "email": "room3@example.com",
            "capacity": 4,
            "features": "",
            "bookable": true,
            "installed_ui_devices": 0,
            "zones": [
                "zone-rGhCRp_aUD"
            ],
            "modules": [
                "mod-rJRNrLDPNz",
                "mod-rJRQ~JwE7U",
                "mod-rJRV1qokbH"
            ],
            "settings": {},
            "created_at": 1562041145,
            "support_url": null,
            "version": 4,
            "id": "sys-rJQVPIR9Uf"
        }
    ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Queries default to searching for any of the entered terms \(words\). A small query language provides the ability to structure complex queries.

| Operator | Action |
| :--- | :--- |
| `+` | Matches both terms. |
| `|`  | Matches either terms. |
| `-` | Negates a single token. |
| `"` | Wraps tokens to form a phrase. |
| `(` and `)` | Provide precedence. |
| `~N` | Specifies edit distance \(fuzziness\) after a word. |
| `~N` | Specifies slop amount \(deviation\) after a phrase. |

## Management

{% api-method method="post" host="https://example.com" path="/api/control/systems" %}
{% api-method-summary %}
Create
{% endapi-method-summary %}

{% api-method-description %}
Defines a new system. Systems names must be unique within the instance they are running on and all systems must have at least one zone associated. All other attributes are optional at the time of creation.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="zones" type="array" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="edge\_id" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="capacity" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="bookable" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="installed\_ui\_devices" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="modules" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="settings" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="support\_url" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "edge_id": "edge-QC03B3OM",
    "name": "Example Room",
    "description": "Example room description containing further cotnext",
    "email": "room@example.com",
    "capacity": 10,
    "features": "",
    "bookable": true,
    "installed_ui_devices": 0,
    "zones": [
        "zone-rGhCRp_aUD"
    ],
    "modules": [],
    "settings": {},
    "created_at": 1562041110,
    "support_url": "https://example.com/foo",
    "id": "sys-rJQQlR4Cn7"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://example.com" path="/api/control/systems/{id}" %}
{% api-method-summary %}
Retrieve
{% endapi-method-summary %}

{% api-method-description %}
Retrieve all metadata associated with the system.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system to retrieve.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="complete" type="boolean" required=false %}
Include full models of all modules and zones associated with the system rather than their ID.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "edge_id": "edge-QC03B3OM",
    "name": "Example Room",
    "description": "Example room description containing further context",
    "email": "room@example.com",
    "capacity": 10,
    "features": "",
    "bookable": true,
    "installed_ui_devices": 0,
    "zones": [
        "zone-rGhCRp_aUD"
    ],
    "modules": [
        "mod-rJRCVYKVuB",
        "mod-rJRGK21pya",
        "mod-rJRHYsZExU"
    ],
    "settings": {},
    "created_at": 1562041110,
    "support_url": "https://example.com/foo",
    "version": 3,
    "id": "sys-rJQQlR4Cn7"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://example.com" path="/api/control/systems/{id}" %}
{% api-method-summary %}
Update
{% endapi-method-summary %}

{% api-method-description %}
Updates system attributes. Any selection of attributes form the request - unspecified items will keep their current values. All requests must include a **version** parameter that matches the current system version.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system to update.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="version" type="integer" required=true %}
The system metadata version. This must match the current version and increments following each successful update.
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="capacity" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="bookable" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="installed\_ui\_devices" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="zones" type="array" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="modules" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="settings" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="support\_url" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "edge_id": "edge-QC03B3OM",
    "name": "Example Room",
    "description": "Example room description containing further context",
    "email": "room@example.com",
    "capacity": 10,
    "features": "",
    "bookable": true,
    "installed_ui_devices": 0,
    "zones": [
        "zone-rGhCRp_aUD"
    ],
    "modules": [],
    "settings": {},
    "created_at": 1562041110,
    "support_url": "https://example.com/foo",
    "id": "sys-rJQQlR4Cn7"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=409 %}
{% api-method-response-example-description %}
The specified version does not match the current system version.
{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://example.com" path="/api/control/systems/{id}" %}
{% api-method-summary %}
Delete
{% endapi-method-summary %}

{% api-method-description %}
Removes a system. This will stop, and remove any modules that are not associated with other systems.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system to retrieve.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Interaction

{% api-method method="post" host="https://example.com" path="/api/control/systems/{id}/start" %}
{% api-method-summary %}
Start
{% endapi-method-summary %}

{% api-method-description %}
Starts all modules associated with the system.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system to start.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://example.com" path="/api/control/systems/{id}/stop" %}
{% api-method-summary %}
Stop
{% endapi-method-summary %}

{% api-method-description %}
Stops all modules associated with the system.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system to stop.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://example.com" path="/api/control/systems/{id}/exec" %}
{% api-method-summary %}
Exec
{% endapi-method-summary %}

{% api-method-description %}
Run behaviour exposed by a module. The associated method will execute and the response returned. If this includes asynchronous or long running behaviour, the result will be awaiting up until a timeout value.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system to execute within.a
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="module" type="string" required=true %}
Class name of the module. i.e. \`Display\`, \`Bookings\` etc
{% endapi-method-parameter %}

{% api-method-parameter name="index" type="integer" required=false %}
\(default 1\) Module index in the system.
{% endapi-method-parameter %}

{% api-method-parameter name="method" type="string" required=true %}
The name of the method to execute.
{% endapi-method-parameter %}

{% api-method-parameter name="args" type="array" required=false %}
Method arguments.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Response values are always wrapped in an outer array. This ensures that method which return primatives \(strings, numbers, booleans or null\) still provide a valid JSON response.
{% endapi-method-response-example-description %}

```javascript
[]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://example.com" path="/api/control/systems/{id}/state" %}
{% api-method-summary %}
State
{% endapi-method-summary %}

{% api-method-description %}
Query the state exposed by a module within the system.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system the module is in.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="module" type="string" required=true %}
Class name of the module.
{% endapi-method-parameter %}

{% api-method-parameter name="index" type="integer" required=false %}
\(default 1\) Index of the module.
{% endapi-method-parameter %}

{% api-method-parameter name="lookup" type="string" required=false %}
A status key of interest. If included, the response filters to this value.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "foo": "abc",
  "bar": 42
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://example.com" path="/api/control/systems/{id}/funcs" %}
{% api-method-summary %}
Funcs
{% endapi-method-summary %}

{% api-method-description %}
Query the behaviour exposed by a module within the system.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system that the module is in.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="module" type="string" required=true %}
Class of the module.
{% endapi-method-parameter %}

{% api-method-parameter name="index" type="integer" required=false %}
\(default 1\) Index of the module.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "function_name": {
    "arity": 1,
    "params": [
      "string"
    ]
  }
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://example.com" path="/api/control/systems/{id}/count" %}
{% api-method-summary %}
Count
{% endapi-method-summary %}

{% api-method-description %}
Counts the instances of a driver type within a system.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system to query.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="module" type="string" required=true %}
Class name of the modules to count.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "count": 3
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://example.com" path="/api/control/systems/{id}/types" %}
{% api-method-summary %}
Types
{% endapi-method-summary %}

{% api-method-description %}
Query the types of modules available within a system.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the system to query.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "Booking": 1,
  "Display": 2,
  "VidConf": 1
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


# Systems

The `/systems` endpoint provides methods for discovering, creating and interacting systems within a deployment. For more on the role that systems play, please see:

{% page-ref page="../../../key-concepts/systems.md" %}

All systems provide a base set of metadata that helps to describe their role and capabilities, as well as provide references to the modules they contain, and the zones they exist in.

## Model

| Attribute | Type | Description |
| :--- | :--- | :--- |
| `id` | string | The system's unique ID. |
| `edge_id` | string | ID of the preferred engine node to run on. |
| `name` | string | The system's primary identifier. |
| `zones` | array | Zone IDs that this system is a member of. |
| `modules` | array | Module ID's that this system contains. |
| `description` | string | Markdown formatted text that describes the system. |
| `email` | string | Calendar email that represents this system. Typically used for room scheduling / bookings. |
| `capacity` | integer | Number of people that can be accommodated in this space. |
| `features` | string | List of features in the room for searching and filtering spaces. |
| `bookable` | boolean | Flag for signifying the space as reservable. |
| `installed_ui_devices` | integer | Expected number of fixed installation touch panels. |
| `settings` | object | JSON object representing the system's configuration. |
| `created_at` | integer | Timestamp of creation time. |
| `support_url` | string | A URL linking to the primary interface for controlling this system. |
| `version` | integer | Incrementing counter for handling stale updates.v |

{% api-method method="get" host="http://aca.example.com" path="/api/control/systems" %}
{% api-method-summary %}
Search
{% endapi-method-summary %}

{% api-method-description %}
Direct queries to the systems endpoint can be used to enumerate, or search for existing systems.
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
A list of systems will be returned, matching the search criteria. If no systems match, an empty list will be provided.
{% endapi-method-response-example-description %}

```
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
]
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Within the query parameter - `q` - a small query language is supported:

| Operator | Action |
| :--- | :--- |
| `+` | Matches both terms. |
| `|` | Matches either terms. |
| `-` | Negates a single token. |
| `"` | Wraps tokens to form a phrase. |
| `(` and `)` | Provide precedence. |
| `~N` | Specifices edit distance \(fuziness\) after a word. |
| `~N` | Specifies slop amount \(deviation\) after a phrase. |

{% api-method method="post" host="https://aca.example.com" path="/api/control/systems" %}
{% api-method-summary %}
Create
{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="edge\_id" type="string" required=true %}
ID of the preferred engine node to run on.
{% endapi-method-parameter %}

{% api-method-parameter name="name" type="string" required=true %}
System name.
{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="email" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="capacity" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="bookable" type="boolean" required=false %}
Default to false
{% endapi-method-parameter %}

{% api-method-parameter name="installed\_ui\_devices" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="zones" type="array" required=true %}

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
    "description": "This is a room that does... things",
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
    "support_url": "https://aca.example.com/foo",
    "id": "sys-rJQQlR4Cn7"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://aca.example/com" path="/api/control/systems/{id}" %}
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
Include full models of all modules and zones associated with the system rather than just ID's.
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
    "description": "This is a room that does... things",
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
    "support_url": "https://aca.example.com/foo",
    "id": "sys-rJQQlR4Cn7"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://aca.example.com" path="/api/control/systems/{id}" %}
{% api-method-summary %}
Update
{% endapi-method-summary %}

{% api-method-description %}
Update system attributes.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=false %}
ID of the system to update.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="version" type="integer" required=true %}
The current system metadata version. This must match the current version attribute of the system and will be incrememented following a successful update.
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
    "description": "This is a room that does... things",
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
    "support_url": "https://aca.example.com/foo",
    "id": "sys-rJQQlR4Cn7"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://aca.example/com" path="/api/control/systems/{id}" %}
{% api-method-summary %}
Delete
{% endapi-method-summary %}

{% api-method-description %}
Remove a system.
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

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


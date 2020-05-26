# Zones

The `/zones` endpoint provide access to discover, create and manage zones available. For more information on the role that zones play, see:

{% page-ref page="../../key-concepts/zones.md" %}

## Model <a id="model"></a>

| Attribute | Type | Description |
| :--- | :--- | :--- |
| id | `string` | Unique ID the represents the zone. |
| name | `string` | Human readable name. |
| description | `string` | Long form description of the zone. |
| tags | `string` | Tags that provide context for the zone use. E.g. `org`, `buidling`, `level`. |
| settings | `object` | JSON object containing configuration linked to this zone. |
| triggers | `array` | List of trigger ID's to be applied to all systems that associate with this zone. |
| created\_at | `integer` | Timestamp of creation. |

## Discovery

{% api-method method="get" host="https://example.com" path="/api/control/zones" %}
{% api-method-summary %}
Search
{% endapi-method-summary %}

{% api-method-description %}
List or search for zones.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-query-parameters %}
{% api-method-parameter name="q" type="string" required=false %}
A search filter to apply.
{% endapi-method-parameter %}

{% api-method-parameter name="limit" type="integer" required=false %}
\(default 20\) Max results to return.
{% endapi-method-parameter %}

{% api-method-parameter name="offset" type="integer" required=false %}
The offset within the result set.
{% endapi-method-parameter %}

{% api-method-parameter name="tags" type="string" required=false %}
Return zones of this tag only.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "total": 3,
  "results": [
    {
        "name": "ACA",
        "description": null,
        "tags": "org",
        "settings": {
            "discovery_info": {
                "buildings": [
                    {
                        "name": "Bourke St",
                        "zone_id": "zone-oOj4O_ijKl"
                    }
                ]
            }
        },
        "triggers": [],
        "created_at": 1555995992,
        "id": "zone-oOj2lGgszq"
    },
    {
        "name": "Bourke St",
        "description": null,
        "tags": "building",
        "settings": {
            "discovery_info": {
                "levels": [
                    {
                        "level_id": "zone-oOj57Msk19",
                        "level_name": "Level 1",
                        "map_url": "assets/maps/level_01.svg"
                    }
                ]
            }
        },
        "triggers": [],
        "created_at": 1555996004,
        "id": "zone-oOj4O_ijKl"
    },
    {
        "name": "Level 1",
        "description": null,
        "tags": "level",
        "settings": {},
        "triggers": [],
        "created_at": 1555996010,
        "id": "zone-oOj57Msk19"
    }
  ]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

Queries default to searching for any of the entered terms \(words\). A small query language provides the ability to structure complex queries.

| Operator | Action |  |
| :--- | :--- | :--- |
| `+` | Matches both terms. |  |
| \` | \` | Matches either terms. |
| `-` | Negates a single token. |  |
| `"` | Wraps tokens to form a phrase. |  |
| `(` and `)` | Provide precedence. |  |
| `~N` | Specifies edit distance \(fuzziness\) after a word. |  |
| `~N` | Specifies slop amount \(deviation\) after a phrase. |  |

## Management

{% api-method method="post" host="https://example.com" path="/api/control/zones" %}
{% api-method-summary %}
Create
{% endapi-method-summary %}

{% api-method-description %}
Defines a new zone.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="tags" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="settings" type="object" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="triggers" type="array" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Zone created.
{% endapi-method-response-example-description %}

```javascript
{
    "name": "ACA",
    "description": null,
    "tags": "org",
    "settings": {},
    "triggers": [],
    "created_at": 1555995992,
    "id": "zone-oOj2lGgszq"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://example.com" path="/api/control/zones/{id}" %}
{% api-method-summary %}
Retrieve
{% endapi-method-summary %}

{% api-method-description %}
Lookup an existing zone.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the zone to retrieve.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "name": "ACA",
    "description": null,
    "tags": "org",
    "settings": {
        "discovery_info": {
            "buildings": [
                {
                    "name": "Bourke St",
                    "zone_id": "zone-oOj4O_ijKl"
                }
            ]
        }
    },
    "triggers": [],
    "created_at": 1555995992,
    "id": "zone-oOj2lGgszq"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://example.com" path="/api/control/zones/{id}" %}
{% api-method-summary %}
Update
{% endapi-method-summary %}

{% api-method-description %}
Updates metadata associated with a zone.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the zone to update.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="tags" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="settings" type="object" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="triggers" type="array" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
    "name": "ACA",
    "description": null,
    "tags": "org",
    "settings": {
        "discovery_info": {
            "buildings": [
                {
                    "name": "Bourke St",
                    "zone_id": "zone-oOj4O_ijKl"
                }
            ]
        }
    },
    "triggers": [],
    "created_at": 1555995992,
    "id": "zone-oOj2lGgszq"
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://example.com" path="/api/control/zones/{id}" %}
{% api-method-summary %}
Delete
{% endapi-method-summary %}

{% api-method-description %}
Removes a zone.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the zone to remove.
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


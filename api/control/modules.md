# Modules

The `/modules` endpoint provides creation, management and direct interaction with modules outside of a system context. For more information on the role that modules play, see:

{% page-ref page="../../key-concepts/modules.md" %}

## Model

<table>
  <thead>
    <tr>
      <th style="text-align:left">Attribute</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">id</td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">A universally unique ID for this module.</td>
    </tr>
    <tr>
      <td style="text-align:left">dependency_id</td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">ID of the driver that defines this module.</td>
    </tr>
    <tr>
      <td style="text-align:left">control_system_id</td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">ID of the system this module is bound to (logic modules only).</td>
    </tr>
    <tr>
      <td style="text-align:left">edge_id</td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">ID of the preferred engine node to run on.</td>
    </tr>
    <tr>
      <td style="text-align:left">ip</td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">IP address or resolvable hostname of the device this module connects to.</td>
    </tr>
    <tr>
      <td style="text-align:left">tls</td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">True if the device communicates securely.</td>
    </tr>
    <tr>
      <td style="text-align:left">udp</td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">Protocol uses UDP rather that TCP.</td>
    </tr>
    <tr>
      <td style="text-align:left">port</td>
      <td style="text-align:left"><code>integer</code>
      </td>
      <td style="text-align:left">The TCP or UDP port that the associated device communicates on.</td>
    </tr>
    <tr>
      <td style="text-align:left">makebreak</td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">If enabled, provides an ephemeral connection that disconnects during idle
        periods.</td>
    </tr>
    <tr>
      <td style="text-align:left">uri</td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">The based URI of the remote service (service modules only).</td>
    </tr>
    <tr>
      <td style="text-align:left">custom_name</td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">The modules class name (<code>Display</code>, <code>Lighting</code> etc)
        if it should differ from the default defined in the dependency.</td>
    </tr>
    <tr>
      <td style="text-align:left">settings</td>
      <td style="text-align:left"><code>object</code>
      </td>
      <td style="text-align:left">A JSON object containing module configuration.</td>
    </tr>
    <tr>
      <td style="text-align:left">updated_at</td>
      <td style="text-align:left"><code>integer</code>
      </td>
      <td style="text-align:left">Timestamp of last update.</td>
    </tr>
    <tr>
      <td style="text-align:left">created_at</td>
      <td style="text-align:left"><code>integer</code>
      </td>
      <td style="text-align:left">Timestamp of creation.</td>
    </tr>
    <tr>
      <td style="text-align:left">role</td>
      <td style="text-align:left"><code>integer</code>
      </td>
      <td style="text-align:left">
        <p>The module type. One of:</p>
        <p><code>0</code> ssh</p>
        <p><code>1</code> device</p>
        <p><code>2</code> service</p>
        <p><code>3</code> logic</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">notes</td>
      <td style="text-align:left"><code>string</code>
      </td>
      <td style="text-align:left">Markdown formatted text that describes this module.</td>
    </tr>
    <tr>
      <td style="text-align:left">connected</td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">Flag for connectivity state.</td>
    </tr>
    <tr>
      <td style="text-align:left">running</td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">Module start/stop state.</td>
    </tr>
    <tr>
      <td style="text-align:left">ignore_connected</td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">If enabled, system metrics ignore connectivity state.</td>
    </tr>
    <tr>
      <td style="text-align:left">ignore_startstop</td>
      <td style="text-align:left"><code>boolean</code>
      </td>
      <td style="text-align:left">If enabled, system level start and stop actions are ignored. This is recommended
        for modules shared by many systems (e.g. a lighting gateway).</td>
    </tr>
  </tbody>
</table>## Discovery

{% api-method method="get" host="https://example.com" path="/api/control/modules" %}
{% api-method-summary %}
Search
{% endapi-method-summary %}

{% api-method-description %}
List or search for existing modules.
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

{% api-method-parameter name="system\_id" type="string" required=false %}
Return modules associated with the specified system.
{% endapi-method-parameter %}

{% api-method-parameter name="dependency\_id" type="string" required=false %}
Return modules that are an instance of the specified dependency.
{% endapi-method-parameter %}
{% endapi-method-query-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "total": 1,
  "results": [
    {
      "dependency_id": "dep-wJHShR4Ffa",
      "control_system_id": null,
      "edge_id": "edge-E9vIruSZ",
      "ip": "10.45.6.3",
      "tls": false,
      "udp": false,
      "port": 8192,
      "makebreak": false,
      "uri": null,
      "custom_name": null,
      "settings": {},
      "updated_at": 1572412023,
      "created_at": 1572392714,
      "role": 1,
      "connected": true,
      "running": true,
      "notes": null,
      "ignore_connected": false,
      "ignore_startstop": false,
      "id": "mod-wJHYeHm6Yn"
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
| `|` | Matches either terms. |
| `-` | Negates a single token. |
| `"` | Wraps tokens to form a phrase. |
| `(` and `)` | Provide precedence. |
| `~N` | Specifies edit distance \(fuzziness\) after a word. |
| `~N` | Specifies slop amount \(deviation\) after a phrase. |

## Management

{% api-method method="post" host="https://example.com" path="/api/control/modules" %}
{% api-method-summary %}
Create
{% endapi-method-summary %}

{% api-method-description %}
Creates a new module.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="dependency\_id" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="edge\_id" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="control\_system\_id" type="string" required=false %}
required for logic modules
{% endapi-method-parameter %}

{% api-method-parameter name="ip" type="string" required=false %}
required for ssh and device modules
{% endapi-method-parameter %}

{% api-method-parameter name="udp" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="port" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="makebreak" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="uri" type="string" required=false %}
required for service modules
{% endapi-method-parameter %}

{% api-method-parameter name="custom\_name" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="settings" type="object" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="notes" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="ignore\_connected" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="ignore\_startstop" type="boolean" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Successful creations will return the full module.
{% endapi-method-response-example-description %}

```javascript
{
  "dependency_id": "dep-wJHShR4Ffa",
  "control_system_id": null,
  "edge_id": "edge-E9vIruSZ",
  "ip": "10.45.6.3",
  "tls": false,
  "udp": false,
  "port": 8192,
  "makebreak": false,
  "uri": null,
  "custom_name": null,
  "settings": {},
  "updated_at": 1572412023,
  "created_at": 1572412023,
  "role": 1,
  "connected": true,
  "running": true,
  "notes": null,
  "ignore_connected": false,
  "ignore_startstop": false,
  "id": "mod-wJHYeHm6Yn"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=406 %}
{% api-method-response-example-description %}
Missing or invalid module configuration.
{% endapi-method-response-example-description %}

```javascript
{
  "dependency_id": ["can't be blank"]
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://example.com" path="/api/control/modules/{id}" %}
{% api-method-summary %}
Retrieve
{% endapi-method-summary %}

{% api-method-description %}
Retrieve all metadata associated with a module.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the modules to retrieve.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "dependency_id": "dep-wJHShR4Ffa",
  "control_system_id": null,
  "edge_id": "edge-E9vIruSZ",
  "ip": "10.45.6.3",
  "tls": false,
  "udp": false,
  "port": 8192,
  "makebreak": false,
  "uri": null,
  "custom_name": null,
  "settings": {},
  "updated_at": 1572412023,
  "created_at": 1572412023,
  "role": 1,
  "connected": true,
  "running": true,
  "notes": null,
  "ignore_connected": false,
  "ignore_startstop": false,
  "id": "mod-wJHYeHm6Yn"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://example.com" path="/api/control/modules/{id}" %}
{% api-method-summary %}
Update
{% endapi-method-summary %}

{% api-method-description %}
Updates module attributes or configuration.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the module to update.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="control\_system\_id" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="edge\_id" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="ip" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="udp" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="port" type="integer" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="makebreak" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="uri" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="custom\_name" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="settings" type="object" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="notes" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="ignore\_connected" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="ignore\_startstop" type="boolean" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Module updated.
{% endapi-method-response-example-description %}

```javascript
{
  "dependency_id": "dep-wJHShR4Ffa",
  "control_system_id": null,
  "edge_id": "edge-E9vIruSZ",
  "ip": "10.45.6.3",
  "tls": false,
  "udp": false,
  "port": 8192,
  "makebreak": false,
  "uri": null,
  "custom_name": null,
  "settings": {},
  "updated_at": 1572412023,
  "created_at": 1572414543,
  "role": 1,
  "connected": true,
  "running": true,
  "notes": null,
  "ignore_connected": false,
  "ignore_startstop": false,
  "id": "mod-wJHYeHm6Yn"
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}
The user does not have permissions to update this module.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}
The passed module ID does not exist.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=406 %}
{% api-method-response-example-description %}
Validation error.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://example.com" path="/api/control/modules/{id}" %}
{% api-method-summary %}
Delete
{% endapi-method-summary %}

{% api-method-description %}
Removes a module. Modules that are associated with multiple systems be removed from all.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the module to delete.
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

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

## Interaction

{% api-method method="post" host="https://example.com" path="/api/control/modules/{id}/start" %}
{% api-method-summary %}
Start
{% endapi-method-summary %}

{% api-method-description %}
Starts a module on it's associated control node.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the module to start.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Module started.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
An error occurred that prevented the module from starting.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://example.com" path="/api/control/modules/{id}/stop" %}
{% api-method-summary %}
Stop
{% endapi-method-summary %}

{% api-method-description %}
Stops the module. Exposed state will still be available but will not update.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the module to stop.
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

{% api-method-response-example httpCode=403 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=404 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="post" host="https://example.com" path="/api/control/modules/{id}/ping" %}
{% api-method-summary %}
Ping
{% endapi-method-summary %}

{% api-method-description %}
Performs a connectivity check with the associated device or service.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the module to check.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "host": "10.45.5.2",
  "pingable": true,
  "warning": null,
  "exception": null
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=406 %}
{% api-method-response-example-description %}
The module specified is a logic module.
{% endapi-method-response-example-description %}

```

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://example.com" path="/api/control/modules/{id}/state" %}
{% api-method-summary %}
State
{% endapi-method-summary %}

{% api-method-description %}
Gets the state information exposed by a module.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the module to query.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-query-parameters %}
{% api-method-parameter name="lookup" type="string" required=false %}
Status key of interest. If included, the response filters to this value.
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


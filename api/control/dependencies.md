# Dependencies

When a driver is loaded into Engine, it becomes a _dependency_. Dependencies are available as the blueprint from which modules are created. The `/dependencies` endpoint provide methods to discover, load and update these. For more on the role the drivers play, see:

{% page-ref page="../../key-concepts/drivers.md" %}

## Model <a id="model"></a>

| Attribute | Type | Description |
| :--- | :--- | :--- |


| id | `string` | The dependency's unique ID. |
| :--- | :--- | :--- |


| name | `string` | Human readable name for the dependency. |
| :--- | :--- | :--- |


| class\_name | `string` | The Ruby class name of the driver. |
| :--- | :--- | :--- |


| module\_name | `string` | The kind of module this instantiates \(e.g. `Display`\). |
| :--- | :--- | :--- |


| role | `string` | One of `ssh`, `device`, `service`, or `logic`. |
| :--- | :--- | :--- |


| description | `string` | Additional information that describes the dependency. |
| :--- | :--- | :--- |


<table>
  <thead>
    <tr>
      <th style="text-align:left">default</th>
      <th style="text-align:left">
        <p><code>string</code> or</p>
        <p><code>integer</code>
        </p>
      </th>
      <th style="text-align:left">A URL or port number that is typical for modules using this.</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>

| ignore\_connected | `boolean` | Default state of connectivity monitoring for instances. |
| :--- | :--- | :--- |


| settings | `object` | A JSON object containing configuration shared by all instances. |
| :--- | :--- | :--- |


| created\_at | `integer` | Timestamp of creation. |
| :--- | :--- | :--- |


{% api-method method="get" host="https://example.com" path="/api/control/dependencies" %}
{% api-method-summary %}
Search
{% endapi-method-summary %}

{% api-method-description %}
List or search for loaded dependencies.
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

{% api-method-parameter name="role" type="string" required=false %}
Filter to a specific role.
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
      "name": "Pexip Management API",
      "description": "Pexip VMR management",
      "role": "service",
      "default": null,
      "class_name": "::Pexip::Management",
      "module_name": "Meeting",
      "ignore_connected": false,
      "settings": {},
      "created_at": 1562041127
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

{% api-method method="post" host="https://example.com" path="/api/control/dependencies" %}
{% api-method-summary %}
Create
{% endapi-method-summary %}

{% api-method-description %}
Defines a new dependency. The driver this references must be available on the engine nodes running this instance of Engine. Available drivers can be listed by using the discovery endpoint.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="class\_name" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="module\_name" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="role" type="string" required=true %}

{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="default" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="ignore\_connected" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="settings" type="object" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Created.
{% endapi-method-response-example-description %}

```javascript
{
  "name": "Pexip Management API",
  "description": "Pexip VMR management",
  "role": "service",
  "default": null,
  "class_name": "::Pexip::Management",
  "module_name": "Meeting",
  "ignore_connected": false,
  "settings": {},
  "created_at": 1562041127
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=406 %}
{% api-method-response-example-description %}
Validation exception.
{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="get" host="https://example.com" path="/api/control/dependencies/{id}" %}
{% api-method-summary %}
Retrieve
{% endapi-method-summary %}

{% api-method-description %}
Gets dependency information
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the dependency to retrieve.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "name": "Pexip Management API",
  "description": "Pexip VMR management",
  "role": "service",
  "default": null,
  "class_name": "::Pexip::Management",
  "module_name": "Meeting",
  "ignore_connected": false,
  "settings": {},
  "created_at": 1562041127
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="put" host="https://example.com" path="/api/control/dependencies/{id}" %}
{% api-method-summary %}
Update
{% endapi-method-summary %}

{% api-method-description %}
Updates dependency metadata.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the dependency to update.i
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}

{% api-method-body-parameters %}
{% api-method-parameter name="name" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="class\_name" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="module\_name" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="role" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="description" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="default" type="string" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="ignore\_connected" type="boolean" required=false %}

{% endapi-method-parameter %}

{% api-method-parameter name="settings" type="object" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Updated.
{% endapi-method-response-example-description %}

```javascript
{
  "name": "Pexip Management API",
  "description": "Pexip VMR management",
  "role": "service",
  "default": null,
  "class_name": "::Pexip::Management",
  "module_name": "Meeting",
  "ignore_connected": false,
  "settings": {},
  "created_at": 1562041127
}
```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=406 %}
{% api-method-response-example-description %}
Validation error.
{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}

{% api-method method="delete" host="https://example.com" path="/api/control/dependencies/{id}" %}
{% api-method-summary %}
Delete
{% endapi-method-summary %}

{% api-method-description %}
Unloads a driver.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the dependency to remove.
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

{% api-method method="post" host="https://example.com" path="/api/control/dependencies/{id}/reload" %}
{% api-method-summary %}
Reload
{% endapi-method-summary %}

{% api-method-description %}
Live reloads the latest version of the driver code and updates all modules using this.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=true %}
ID of the dependency to reload.
{% endapi-method-parameter %}
{% endapi-method-path-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}
Reload successful.
{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}

{% api-method-response-example httpCode=500 %}
{% api-method-response-example-description %}
An error was detected in the updated driver and the reload is blocked. If this occurs, the previously operating driver will continue to run uninterrupted.
{% endapi-method-response-example-description %}

```text

```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}


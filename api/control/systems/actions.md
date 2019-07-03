---
description: >-
  Within the context of a system, a number of actions are possible that interact
  with the modules it contains.
---

# Module Interaction

{% api-method method="post" host="https://aca.example.com" path="/api/control/systems/{id}/start" %}
{% api-method-summary %}
Start all modules
{% endapi-method-summary %}

{% api-method-description %}
Starts all modules contained in the specified system.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=false %}
ID of the system to start.
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

{% api-method method="post" host="https://aca.example.com" path="/api/control/systems/{id}/stop" %}
{% api-method-summary %}
Stop all modules
{% endapi-method-summary %}

{% api-method-description %}
Stops and deactivates all modules in the specified system.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=false %}
ID of the system to stop.
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

{% api-method method="post" host="https://aca.example.com" path="/api/control/systems/{id}/exec" %}
{% api-method-summary %}
Execute a module method
{% endapi-method-summary %}

{% api-method-description %}
Run behaviour that has been exposed by a module.
{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-path-parameters %}
{% api-method-parameter name="id" type="string" required=false %}
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
The name of the method that should be executed.
{% endapi-method-parameter %}

{% api-method-parameter name="args" type="array" required=false %}
Argument to be sent to the method.
{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
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




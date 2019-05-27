# Authentication

Access to ACAEngine is secured via [OAuth2](https://www.oauth.com/). Before interacting with either the REST or Realtime API's you must first authenticate and obtain an access token. Once authenticated, this token must accompany all requests.

## Registering Your Application

To support external interaction all applications using ACAEngine API's need to be registered in Backoffice. Further details on this can be found in the Backoffice user guide.

{% page-ref page="../backoffice.md" %}

## Obtaining An Access Token

Depending on your application requirements, a number of approaches are available to authenticate.



### Password Grant

The password grant flow provides an option for server-to-server integration, or when designing a system where direct knowledge of both user, and application auth information is acceptable. It should not be user as part of any client / user accessible code. This flow provides the ability to directly exchange a username and password for an access token as a single request.

{% api-method method="post" host="https://aca.example.com" path="/auth/oauth/token" %}
{% api-method-summary %}

{% endapi-method-summary %}

{% api-method-description %}

{% endapi-method-description %}

{% api-method-spec %}
{% api-method-request %}
{% api-method-body-parameters %}
{% api-method-parameter name="grant\_type" type="string" required=true %}
"password"
{% endapi-method-parameter %}

{% api-method-parameter name="username" type="string" required=true %}
The user to authenticate as.
{% endapi-method-parameter %}

{% api-method-parameter name="password" type="string" required=true %}
The password to authenticate with.
{% endapi-method-parameter %}

{% api-method-parameter name="authority" type="string" required=true %}
The authority ID to authenticate against.
{% endapi-method-parameter %}

{% api-method-parameter name="client\_id" type="string" required=true %}
Application client ID.
{% endapi-method-parameter %}

{% api-method-parameter name="client\_secret" type="string" required=true %}
Application client secret.
{% endapi-method-parameter %}

{% api-method-parameter name="scope" type="string" required=false %}

{% endapi-method-parameter %}
{% endapi-method-body-parameters %}
{% endapi-method-request %}

{% api-method-response %}
{% api-method-response-example httpCode=200 %}
{% api-method-response-example-description %}

{% endapi-method-response-example-description %}

```javascript
{
  "access_token": "1f0af717251950dbd4d73154fdf0a474a5c5119adad999683f5b450c460726aa",
  "token_type": "bearer",
  "expires_in": 7200
}
```
{% endapi-method-response-example %}
{% endapi-method-response %}
{% endapi-method-spec %}
{% endapi-method %}




# Realtime API

The real-time API is the primary method for interacting with devices managed by ACA Engine. It uses a WebSocket connection to allow you to build efficient, responsive user interfaces, monitoring systems and other extensions which require live, two-way or asynchronous interaction.

If you are building browser-based experiences we have a pre-built AngularJS client library ready to go:

{% page-ref page="../../developer-guide/user-interfaces/composer.md" %}

Otherwise, if you are working with other frameworks, or would like to build your own, read on.

## Opening the Connection

A connection to the real-time API can be established by requesting the `/control/websocket` endpoint with valid access token. The method for this will vary depending on the tooling used for your app, but as a simple example in JavaScript this can be achieved by creating a new WebSocket object:

```javascript
let socket = new WebSocket('wss://aca.example.com/control/websocket?bearer_token=<access token>');
```

 When opened, this will provide a full-duplex stream for communications.


---
description: The Zilla Server-sent Events (SSE) Kafka Proxy exposes an SSE stream of Kafka messages.
prev: false
next: /tutorials/sse/sse-intro.md
---

# SSE Kafka Proxy

The Zilla Server-sent Events (SSE) Kafka Proxy exposes an SSE stream of Kafka messages.

An [SSE](https://html.spec.whatwg.org/multipage/server-sent-events.html) server allows a web browser using the `EventSource` interface to open a connection and receive a stream of text from the server, interpreted as individual messages. Zilla relays text messages on a Kafka topic into the event stream. Individual Kafka topics can be mapped to the client connection path.

## Message Filtering

Messages from Kafka are mapped using a route that will define a path for the client to connect and the topic for the messages. A route can [filter](../../reference/config/bindings/binding-sse-kafka.md#routes-with) messages delivered to the SSE stream using the message key and headers. A filter's value can be statically defined in the config or be a dynamic segment of the HTTP path used when the client connects.

## Reliable Delivery

Zilla sends the event id and last-event-id header to recover from an interrupted stream without message loss and without needing the client to acknowledge message receipt explicitly.

## Continuous Authorization

Like the [REST Proxy](./rest-proxy.md), you can secure `SSE` endpoints. Unlike HTTP, which authorizes individual requests, Zilla continuously authorizes the long-lived SSE connection stream. Zilla will send a "challenge" event, triggering the client to send up-to-date authorization credentials, such as a JWT token, before expiration. Zilla adheres to the secure by default method meaning, if authorization expires before the client responds to the "challenge" event, then the response stream is terminated.

Multiple SSE streams on the same HTTP/2 connection and authorized by the same JWT token are reauthorized by a single "challenge" event response from the client. They are all terminated if the token expiration isn't updated.

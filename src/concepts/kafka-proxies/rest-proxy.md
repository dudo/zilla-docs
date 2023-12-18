---
description: Zilla lets you configure application-centric REST API endpoints that unlock Kafka event-driven architectures.
prev: false
next: /tutorials/rest/rest-intro.md
---

# REST Kafka Proxy

Zilla lets you configure application-centric REST API endpoints that unlock Kafka event-driven architectures. An application-centric REST API for Kafka gives the developer freedom to define their own HTTP mapping to Kafka, with control over the topic, message key, message headers, message value, and reply-to topic. This guide will explain all the aspects of configuring Zilla with REST API endpoints.

## Configure Endpoints

Zilla can be configured to map REST APIs to Kafka using the [http-kafka](../../reference/config/bindings/binding-http-kafka.md) binding in `zilla.yaml`.

Kafka **Produce** capability and HTTP request method types such as `POST`, `PUT`, `DELETE`, and `PATCH` .

::: info NOTE
When the POST request is received by Zilla, a message is produced to the requests topic, with HTTP headers delivered as the Kafka message headers and the HTTP payload delivered as the Kafka message value. You have the option to [override headers](../../reference/config/bindings/binding-http-kafka.md#capability-produce) as well.
:::

Kafka **Fetch** capability with HTTP request methods such as `GET` :

### Dynamic URL parameters

Zilla can map URL path params and headers, e.g. `/tasks/123` could extract the id `123`. 

## Correlated Request-Response

Zilla manages the HTTP lifecycle with both the request and response payload represented with on the event stream. Each message is correlated to each other with a `zilla:correlation-id` header enabling both Zilla and Kafka workflows to act based on the use case. Correlated messages can be on the same or different Kafka topics

### sync

A synchronous interaction from the client will hold the connection open waiting for the correlated response message to be delivered to the caller.

### async

An asynchronous interaction is managed over a pair of Kafka topics. An initiating request returns can include a `prefer: respond-async` header which will immediately with `202 Accepted` plus the location to retrieve a correlated response. A waiting request can then send a request including the `prefer: wait=N` header to retrieve the correlated response as soon as it becomes available, this removes the need for client polling.

## Oneway

Clients can produce an HTTP request payload to a Kafka topic. A Kafka message key and/or headers can be set using `${params}` from the HTTP path.

## Cache

Retrieve message from a Kafka topic, filtered by message key and/or headers, with key and/or header values extracted from segments of the HTTP path if needed.

Returns an `etag` header with HTTP response. Supports conditional `GET if-none-match request`, returning `304` if not modified or `200` if modified (with a new `etag` header). Supports `prefer: wait=N` to respond as soon as messages become available, no need for client polling.

## CORS

Zilla supports Cross-Origin Resource Sharing (CORS) and allows you to specify fine-grained access control including specific request origins, methods and headers allowed, and specific response headers exposed. Since it acts more like a guard and has no dependency on Apache Kafka configuration, you need to define it in the [http](../../reference/config/bindings/binding-http.md) binding.

## Authorization

Since `Zilla` config is very much modular it has the concept of [`guard`](../../reference/config/overview.md#guards) where you define your `guard` configuration and reference that `guard` to authorize a specific endpoint. Currently, `Zilla` supports JSON Web Token (JWT) authorization with the [`jwt`](../../reference/config/guards/guard-jwt.md) Guard.

The information about keys and other details such as issuer and audience you can get from `JWT` providers for example in the case of Auth0 you can use the command below.

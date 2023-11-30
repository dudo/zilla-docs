---
description: Running these Zilla samples will introduce some REST features.
---

# REST Intro

Get started with Zilla by deploying our Docker Compose stack. Before proceeding, you should have [Docker Compose](https://docs.docker.com/compose/gettingstarted/) installed.

## CRUD on a Kafka event stream

Running this Zilla sample will create a simple API to create and list items. All of the data will be stored on a Kafka topic.

### Setup

Create these files, `zilla.yaml` and `docker-compose.yaml`, in the same directory.

::: code-tabs#yaml

@tab zilla.yaml

```yaml {28,32-33,35,39-40}
<!-- @include: ./zilla.yaml -->
```

@tab docker-compose.yaml

```yaml
<!-- @include: ./docker-compose.yaml -->
```

:::

### Run Zilla and Kafka

```bash:no-line-numbers
docker-compose up -d
```

### Use `curl` to send a greeting

```bash:no-line-numbers
curl -X POST http://localhost:7114/items -H 'Content-Type: application/json' -d '{"greeting":"Hello, world"}'
```

### Use `curl` to list all of the greetings

```bash:no-line-numbers
curl http://localhost:7114/items
```

```output:no-line-numbers
[{"greeting":"Hello, world"}]
```

### Remove the running containers

```bash:no-line-numbers
docker-compose down
```

::: tip See more of what Zilla can do
Go deeper into this concept with the [http.kafka.crud](https://github.com/aklivity/zilla-examples/tree/main/http.kafka.crud) example.
:::

## Going Deeper

Try out more HTTP examples:

- [http.echo](https://github.com/aklivity/zilla-examples/tree/main/http.echo)
- [http.echo.jwt](https://github.com/aklivity/zilla-examples/tree/main/http.echo.jwt)
- [http.proxy](https://github.com/aklivity/zilla-examples/tree/main/http.proxy)
- [http.filesystem](https://github.com/aklivity/zilla-examples/tree/main/http.filesystem)
- [http.filesystem.config.server](https://github.com/aklivity/zilla-examples/tree/main/http.filesystem.config.server)
- [http.kafka.async](https://github.com/aklivity/zilla-examples/tree/main/http.kafka.async)
- [http.kafka.cache](https://github.com/aklivity/zilla-examples/tree/main/http.kafka.cache)
- [http.kafka.crud](https://github.com/aklivity/zilla-examples/tree/main/http.kafka.crud)
- [http.kafka.oneway](https://github.com/aklivity/zilla-examples/tree/main/http.kafka.oneway)
- [http.kafka.sasl.scram](https://github.com/aklivity/zilla-examples/tree/main/http.kafka.sasl.scram)
- [http.kafka.sync](https://github.com/aklivity/zilla-examples/tree/main/http.kafka.sync)


rest-kafka-1       | {"time":"2023-11-30T16:41:32.892647721Z","level":"ERROR","msg":"http_response","git_commit":"0344e8d30fdc194497aafd38a1fa5cde9a995eeb","git_time":"2023-11-29T21:35:46Z","git_modified":true,"go_os":"linux","go_arch":"arm64","process_generation":"598325ad-5987-452d-a23d-81098342d945","hostname_fqdn":"kafka","hostname_short":"kafka","private_ips":["192.168.112.2"],"num_vcpus":4,"kinesis_enabled":true,"kafka_enabled":true,"module":"kinesis","amz_request_id":"51bc33b4-8f9f-11ee-8663-0242c0a87002","amz_id_2":"CeiA5F5opZ40g5yZuyLTYdjRPXp7qO8dgnlJeqfgP5I0WA934HtGRAvOlNZ5icEcJ7G1z5RWWI8I/9yU8InOz4Ez0PxCwSSm","amz_target":"","aws_sdk_invocation_id":"","http_method":"GET","http_content_type":"","http_user_agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36","http_expect":"","http_content_length":0,"error":{"message":"kind: AccessDeniedException, message: Unable to determine service/operation name to be authorized., internal: , json: {\"__type\":\"AccessDeniedException\",\"message\":\"Unable to determine service/operation name to be authorized.\"}"},"duration_ms":0,"amz_error_type":"AccessDeniedException","amz_error_message":"Unable to determine service/operation name to be authorized."}
rest-kafka-1       | {"time":"2023-11-30T16:41:36.386588Z","level":"ERROR","msg":"http_response","git_commit":"0344e8d30fdc194497aafd38a1fa5cde9a995eeb","git_time":"2023-11-29T21:35:46Z","git_modified":true,"go_os":"linux","go_arch":"arm64","process_generation":"598325ad-5987-452d-a23d-81098342d945","hostname_fqdn":"kafka","hostname_short":"kafka","private_ips":["192.168.112.2"],"num_vcpus":4,"kinesis_enabled":true,"kafka_enabled":true,"module":"kinesis","amz_request_id":"53d15723-8f9f-11ee-8663-0242c0a87002","amz_id_2":"pVmX1Jh9pSz3mf4lkVn/x9JgGqrkoNZ6f3xBm7KYPCR9gASDBbBqRZPoTC7CcuPMj1PLTa72Tkhl+8LHRyJX3gQno8EGI0n3","amz_target":"","aws_sdk_invocation_id":"","http_method":"GET","http_content_type":"","http_user_agent":"Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/119.0.0.0 Safari/537.36","http_expect":"","http_content_length":0,"error":{"message":"kind: AccessDeniedException, message: Unable to determine service/operation name to be authorized., internal: , json: {\"__type\":\"AccessDeniedException\",\"message\":\"Unable to determine service/operation name to be authorized.\"}"},"duration_ms":0,"amz_error_type":"AccessDeniedException","amz_error_message":"Unable to determine service/operation name to be authorized."}
^CGracefully stopping... (press Ctrl+C again to force)

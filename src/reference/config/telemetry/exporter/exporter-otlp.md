---
shortTitle: open telemetry
description: Zilla runtime otlp exporter
category:
  - Telemetry
tag:
  - Exporters
---

# Open Telemetry Exporter

Zilla runtime Open Telemetry exporter

```yaml {3}
exporters:
  otlp:
    type: otlp
    options:
      interval: 30
      signals:
        - metrics
      endpoint:
        protocol: http
        location: http://otlp-collector:4318/v1/metrics
```

## Configuration

:::: note Properties

- [options\*](#options)
  - [options.interval](#options-interval)
  - [options.signals](#options-signals)
  - [options.endpoint\*](#options-endpoint)
    - [endpoint.protocol](#endpoint-protocol)
    - [endpoint.location\*](#endpoint-location)

::: right
\* required
:::

::::

### options*

> `object`

`otlp`-specific options.

```yaml
options:
  interval: 30
  signals:
    - metrics
  endpoint:
    protocol: http
    location: http://otlp-collector:4318/v1/metrics
```

#### options.interval

> `integer`

Interval in seconds to push data to the Open Telemetry collector. Default: 30 seconds.

#### options.signals

> `array` of `strings`

Specifies what signals should be exported. Currently only `metrics` is supported. The default
behaviour is to export all supported signals.

#### options.endpoint*

> `object`

Contains details for the Open Telemetry collector endpoint.

##### endpoint.protocol

> `string`

Specifies the protocol to use for exporting data. Currently only `http` is supported. The default is `http`.

##### endpoint.location*

> `string`

The URL of the Open Telemetry collector.

---

::: right
\* required
:::

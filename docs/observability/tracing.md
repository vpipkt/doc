---
description: >-
  Application Performance Monitoring or tracing using Grafana Tempo on NAIS.
---

# Tracing

!!! info "Status: Beta"
    **Experimental**: users report that this component is working, but it needs a broader audience to be battle-tested properly.

    Please report any issues to the #nais channel on Slack.

!!! info "New Grafana URL"
    When visualizing traces, you must use the new Grafana instance at https://grafana.nav.cloud.nais.io.

Traces are a record of the path a request takes through your application. They
are useful for understanding how a request is processed in your application.

NAIS does not collect trace data automatically. If you want tracing integration,
you must first instrument your application to collect traces, and then configure
the tracing library to send it to the correct place.

Traces from NAIS applications are collected using the [OpenTelemetry](https://opentelemetry.io/) standard.
Performance metrics are stored and queried from the [Tempo](https://grafana.com/oss/tempo/) component.

This documentation applies to backend applications. If you need to enable
tracing for end users in their browser, see [frontend observability](https://doc.nais.io/observability/frontend/).

## Enabling trace collection

The first step in collecting trace information is to enable it in your application spec:

=== "nais.yaml"
    ```yaml
    spec:
      observability:
        tracing:
          enabled: true
    ```

Next, you must select the appropriate [OTLP exporter](https://opentelemetry.io/ecosystem/registry/?s=otlp+exporter)
for your specific application. Ready-made libraries can be found for Java, Rust, Python, Go, and most other popular languages.
Detailed instructions on how to configure specific tracing libraries are out of scope for this documentation.

Finally, the OTLP exporter must be configured to send data to the NAIS collector.
That configuration is provided by NAIS through the `$OTEL_EXPORTER_OTLP_ENDPOINT` environment variable,
which in turn is supposed to be automatically detected and used by your OpenTelemetry library.
All data must be sent using the gRPC protocol.


## Visualizing application performance

Visualization of traces can be done in [the new Grafana installation](https://grafana.nav.cloud.nais.io).

You can use the **Explore** feature of Grafana with the _prod-gcp-tempo_ and _dev-gcp-tempo_ data sources.

There are no ready-made dashboards at this point, but feel free to make one yourself and contribute to this page.

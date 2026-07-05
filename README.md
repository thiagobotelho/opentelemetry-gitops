# opentelemetry-gitops

Red Hat build of OpenTelemetry para OpenShift Local. O Collector recebe OTLP
em `4317/4318`, limita memória, agrupa spans e envia traces ao
`TempoMonolithic`.

```bash
oc apply -k overlays/crc
```

Aplicações devem exportar para:

```text
http://otel-collector-collector.observability.svc:4318
```

Referência: documentação Red Hat build of OpenTelemetry do OpenShift 4.20.

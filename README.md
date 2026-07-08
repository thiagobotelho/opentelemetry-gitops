# opentelemetry-gitops

Red Hat build of OpenTelemetry para OpenShift Local. O Collector recebe OTLP
em `4317/4318`, limita memória, agrupa spans e envia traces ao
`TempoMonolithic`.

```bash
oc apply -k overlays/desenvolvimento
```

Aplicações devem exportar para:

```text
http://otel-collector-collector.observability.svc:4318
```

Referência: documentação Red Hat build of OpenTelemetry do OpenShift 4.20.

## Ambientes e validação

```bash
oc kustomize overlays/desenvolvimento >/tmp/otel-dev.yaml
oc kustomize overlays/aceite >/tmp/otel-aceite.yaml
oc kustomize overlays/producao >/tmp/otel-prod.yaml
oc apply --dry-run=client -k overlays/desenvolvimento
```

O exporter Tempo aponta para
`tempo-tempo-monolithic-gateway.tempo.svc.cluster.local:4317`. Ajuste por
overlay se o namespace/nome do Tempo mudar. Mais detalhes em
`docs/AMBIENTES.md`.

## Automatizações preservadas e ajustadas

- `.github/workflows/validate.yml` foi preservado e ajustado para renderizar
  todos os Kustomizations, não apenas `overlays/crc`.
- O overlay legado `overlays/crc` permanece como compatibilidade; use
  `overlays/desenvolvimento` como padrão.

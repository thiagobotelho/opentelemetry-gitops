# Ambientes

Este repositório usa `base/` e `overlays/{desenvolvimento,aceite,producao}`.

- `desenvolvimento`: Collector em modo `deployment`, uma réplica e recursos reduzidos para CRC.
- `aceite`: mesmo desenho com espaço para patchar réplicas, recursos, filas e exporters.
- `producao`: exige revisão de HA, retries, autenticação/TLS, resource sizing e separação de tenants.

Validação:

```bash
oc kustomize overlays/desenvolvimento >/tmp/otel-dev.yaml
oc kustomize overlays/aceite >/tmp/otel-aceite.yaml
oc kustomize overlays/producao >/tmp/otel-prod.yaml
oc apply --dry-run=client -k overlays/desenvolvimento
```

Integrações:

- Receivers OTLP gRPC/HTTP em `4317/4318`.
- Exporter OTLP gRPC para `tempo-tempo-monolithic-gateway.tempo.svc.cluster.local:4317`.
- Connector `span_metrics` expõe métricas RED em `8889` para Prometheus.

Automação preservada:

- `.github/workflows/validate.yml`: agora renderiza todos os Kustomizations e executa `yamllint`.

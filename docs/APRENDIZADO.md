# Pipeline de telemetria


receivers recebem OTLP; memory_limiter limita pressão de memória; batch agrupa spans; exporters enviam ao destino. O bearer token identifica o Collector no Tempo; a CA autentica o servidor. Antes de exportar, filtre atributos que possam conter dados pessoais, tokens ou parâmetros sensíveis. Teste com spans sintéticos sem dados reais.

## Diagnosticar exportação do mesh

Confira descoberta do Service OTLP pelo Istiod, configuração de tracing no Envoy, recepção no Collector e consulta no tenant Tempo. Um trace_id no log não garante exportação: a decisão de amostragem e a saúde do pipeline precisam ser verificadas. O roteiro integrado está no guia de observabilidade de service-mesh-gitops.

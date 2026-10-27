# Pipeline de telemetria

## O que observar

receivers recebem OTLP; memory_limiter limita pressão de memória; batch agrupa spans; exporters enviam ao destino. O bearer token identifica o Collector no Tempo; a CA autentica o servidor. Antes de exportar, filtre atributos que possam conter dados pessoais, tokens ou parâmetros sensíveis. Teste com spans sintéticos sem dados reais.

## Roteiro de leitura e validação

1. Leia o README e identifique o componente que recebe a configuração.
2. Confira namespaces, seletores, portas, identidades e dependências nos exemplos.
3. Ajuste apenas os campos necessários em um ambiente isolado; não use credenciais de produção.
4. Valide sintaxe e contratos locais antes de aplicar. Registre o resultado real separado deste guia.
5. Execute um caso permitido e um caso negado, conferindo a causa da resposta.
6. Defina reversão por recurso/arquivo e preserve dados persistentes antes de mudanças.

Os comentários dos manifests explicam escolhas; não comprovam disponibilidade do componente. Exemplos fora de entradas Kustomize não são implantados automaticamente.

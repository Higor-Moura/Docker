# DaemonSet no Kubernetes

## O que é?

Um **DaemonSet** é um recurso do Kubernetes usado para garantir que **uma cópia de um Pod seja executada em todos (ou em alguns) Nodes** do cluster.

## Para que serve um DaemonSet?

- Implantar **agentes de monitoramento** (ex: Prometheus Node Exporter)
- Implantar **coletores de logs** (ex: Fluentd, Filebeat)
- Rodar **ferramentas de segurança** ou **infraestrutura de rede**
- Execução de containers que precisam estar presentes em todos os nodes

## Como funciona?

- Cria automaticamente um Pod **em cada Node**.
- Se um novo Node for adicionado ao cluster, o DaemonSet cria um Pod nele.
- Se um Node for removido, os Pods do DaemonSet naquele Node são automaticamente deletados.


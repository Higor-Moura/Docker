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

---

 ARQUIVO DE EXEMPLO:
 
```
apiVersion: apps/v1
kind: DaemonSet
metadata:
  name: my-daemonset
  labels:
    app: frontend

spec:
  template:
    metadata:
      name: pod-web-server
      labels:
        apps: my-app
        tier: frontend
    spec:
      containers:
        - name: my-container-nginx
          image: nginx

  selector:
    matchLabels:
      apps: my-app
```

## Verificando se o daemonset realmente criou um pod em cada node 

- Check os nodes disponiveis

```
kubectl get nodes
```
> Voce tera uma saida com os nomes dos nodes

- VERIFICANDO SE OS PODS FORAM ALOCADOS NOS NODES

```
kubectl get pods -o wide --field-selector spec.nodeName=<nome do node>
```

> - Se quiser verificar o outro node basta mudar o nome do node

# DAEMONSET ORPHAN PODS
- > O que é? Um Orphan Pod (Pod órfão) é um Pod que perdeu seu controlador, ou seja, não está mais vinculado a um Daemonset

- DaemonSet Deletion
- --cascade=orphan Option
- DaemonSet Adoption

## Deletando o DaemonSet com o orphan pods 

```
kubectl delete daemonset <nome do daemonset> --cascade=orphan
```

# ReplicaSet

> O propósito de um ReplicaSet é gerenciar um conjunto de réplicas de Pods em
> execução a qualquer momento. Por isso, é geralmente utilizado para garantir a
> disponibilidade de um certo número de Pods idênticos.

**Se um pod chegar a cair por algum motivo o replicaset sobe outro identico para manter a disponibilidade**

#### Crie o arquivo replica set 

```
sudo vi /etc/kubernetes/manifest/replicaset.yml
```
**conteudo do arquivo**

```
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend-rs
  labels:
    app: frontend
# Especificações do replicaset
spec:
  template:
    metadata:
      name: pod-webserver
      labels:
        apps: my-apps
        tier: frontend
# Especificações do container
    spec:
      containers:
      - name: nginx
        image: nginx
# Responsavel por selecionar em qual pod o replicaset vai controlar as replicas
  selector:
    matchLabels:
# Selecionando a labels criada la em spec
      apps: my-apps
# Definindo a quantidade de pod que deseja criar 
  replicas: 4
```

#### Verifique se subiu as 4 PODs

```
kubectl get pods
```

#### Teste o Replicaset delete um POD e verifica se o ReplicaSet sobe outra 

```
kubectl delete pods <nome do pod>
```
**agora verifique os pods novamente, e veja se o replicaset subiu**

> - Pode ate apagar todas as PODs o replicaset vai subir novamente
> - Mas se apagar o replicaset todos os PODs por ele criado são deletados automaticamente 

# ReplicaSet Scale

> - Capacidade de aumentar ou diminuir a quantidade de PODs dentro do sistema
> - Basta aumentar ou diminuir a quantidade de `replicas` no final do arquivo `replicaset.yml`
> - Feito isso so executar `kubectl apply -f replicaset.yml`

**Dessa forma voce muda pelo arquivo, mas tambem tem a opção de fazer por comando**

#### Scale por comando

```
kubectl scale replicasets frontend-rs --replicas=5 
```

> - `kubectl scale replicasets` = Comando para executar o scale
> - `frontend-rs` = Nome do replicaset que voce quer executar o scale
> - `--replicas=5` = Especifique quantas replicas voce deseja








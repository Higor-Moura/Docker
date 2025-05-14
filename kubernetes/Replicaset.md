
# ReplicaSet

> O propósito de um ReplicaSet é gerenciar um conjunto de réplicas de Pods em execução a qualquer momento. Por isso, é geralmente utilizado para garantir a disponibilidade de um certo número de Pods idênticos.

**Se um pod chegar a cair por algum motivo o ReplicaSet sobe outro idêntico para manter a disponibilidade.**

---

### Criação do ReplicaSet

```bash
sudo vi /etc/kubernetes/manifest/replicaset.yml
```

**Conteúdo do arquivo**

```yaml
apiVersion: apps/v1
kind: ReplicaSet
metadata:
  name: frontend-rs
  labels:
    app: frontend
spec:
  replicas: 4
  selector:
    matchLabels:
      apps: my-apps
  template:
    metadata:
      name: pod-webserver
      labels:
        apps: my-apps
        tier: frontend
    spec:
      containers:
        - name: nginx
          image: nginx
```

---

### Verifique se subiu os 4 Pods

```bash
kubectl get pods
```

### Teste o ReplicaSet: delete um Pod e veja se o ReplicaSet sobe outro

```bash
kubectl delete pods <nome-do-pod>
kubectl get pods
```

> Pode até apagar todas as Pods, o ReplicaSet vai recriar.  
> Mas se apagar o ReplicaSet, **todos os Pods por ele criados serão deletados automaticamente.**

---

## Escalando o ReplicaSet

> O ReplicaSet permite aumentar ou diminuir a quantidade de Pods.  
> Basta alterar o valor de `replicas` no arquivo `replicaset.yml` e aplicar novamente:

```bash
kubectl apply -f replicaset.yml
```

### Escalando via linha de comando

```bash
kubectl scale replicasets frontend-rs --replicas=5
```

- `kubectl scale replicasets` → Comando para escalar
- `frontend-rs` → Nome do ReplicaSet
- `--replicas=5` → Define a nova quantidade de réplicas

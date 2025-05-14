# Kubernetes Deployments

## O que é um Deployment?

Um **Deployment** gerencia a criação e atualização de **Pods** em um cluster Kubernetes. Ele permite escalabilidade, atualizações controladas e rollback de versões com segurança.

### Estratégias de Atualização

- **Rolling Update (Padrão)**  
  Atualiza os Pods gradualmente, garantindo alta disponibilidade.  
  Por padrão, permite:
  - **25% de indisponibilidade máxima** (`maxUnavailable`)
  - **25% de pods extras temporários** (`maxSurge`)

  Exemplo: Com 4 Pods em execução, apenas 1 será substituído por vez, mantendo no mínimo 3 ativos durante a atualização.

- **Recreate**  
  Todos os Pods são terminados antes dos novos serem criados. Pode causar **indisponibilidade temporária**.

- **Rollback**  
  Caso uma nova versão apresente falhas, é possível voltar para a versão anterior com segurança.

---

## Criando um Deployment

### Arquivo `deployment-teste.yml`

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-deployment
  labels:
    app: frontend
spec:
  replicas: 4
  selector:
    matchLabels:
      env: production
  template:
    metadata:
      name: pod-my-nginx
      labels:
        env: production
    spec:
      containers:
        - name: nginx-container
          image: nginx
```

### Aplicando o Deployment

```bash
kubectl apply -f deployment-teste.yml
```

### Verificando o Deployment

```bash
kubectl get deployment
kubectl get replicaset
```

---

## Deployment Rollout

O **rollout** é o processo de atualização de um Deployment com uma nova versão da aplicação. O Kubernetes garante que a troca aconteça sem downtime.

### Comando para verificar status do rollout

```bash
kubectl rollout status deployment.apps/frontend-deployment
```

### Comando para ver detalhes do Deployment

```bash
kubectl describe deployment.apps/frontend-deployment
```

> Nos detalhes, observe:
> - `RollingUpdateStrategy`: mostra a estratégia em uso
> - `maxUnavailable`: percentual máximo de pods indisponíveis simultaneamente
> - `maxSurge`: número máximo de pods extras criados durante a atualização

---

## Rollout History

Mostra o histórico de revisões do Deployment.

### Ver histórico de versões

```bash
kubectl rollout history deployment.apps/frontend-deployment
```

### Ver detalhes de uma revisão específica

```bash
kubectl rollout history deployment.apps/frontend-deployment --revision=2
```

---

## Deployment Rollback

Permite reverter para uma versão anterior.

### Rollback para a última versão

```bash
kubectl rollout undo deployment.apps/frontend-deployment
```

### Rollback para uma versão específica

```bash
kubectl rollout undo deployment.apps/frontend-deployment --to-revision=5
```

---

## Rollout Pause & Resume

Pause e retome atualizações de um Deployment manualmente.

### Pausar o rollout

```bash
kubectl rollout pause deployment.apps/frontend-deployment
```

### Retomar o rollout

```bash
kubectl rollout resume deployment.apps/frontend-deployment
```

---

## Scale Up & Down

Ajuste o número de réplicas do Deployment.

```bash
kubectl scale deployment.apps/frontend-deployment --replicas=11
```

> Use esse comando para aumentar ou diminuir a quantidade de Pods rodando.

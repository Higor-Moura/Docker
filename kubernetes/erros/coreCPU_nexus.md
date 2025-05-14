# Corrigindo Erro de CPU no Nexus no Kubernetes

Ao executar o Nexus em um ambiente Kubernetes com recursos limitados, você pode se deparar com a seguinte mensagem de erro:

- The host system is allocating a maximum of 1 cores to the application.A minimum of 4 is recommended

![Captura de tela de 2025-05-14 08-56-50](https://github.com/user-attachments/assets/c2b8e480-e90c-4163-b5b6-67d16284194f)

---

## Solução

- É necessário alocar pelo menos **4 CPUs** para o container do Nexus. Isso é feito especificando os recursos no `deployment.yaml`.

### Parte de configuração de recursos

```
resources:
  requests:
    cpu: "4"
    memory: "4Gi"
  limits:
    memory: "4Gi"
    cpu: "4"
```
### Explicação 

- `requests:` Define a quantidade mínima de CPU e memória que o container requisita ao iniciar.
- `limits:`  Define a quantidade máxima de CPU e memória que o container pode utilizar.
  
# Exemplo completo de arquivo `deployment.yaml`

```

apiVersion: apps/v1
kind: Deployment
metadata:
  name: nexus
  namespace: nexus-3
spec:
  replicas: 2
  selector:
    matchLabels:
      app: setup
  template:
    metadata:
      labels:
        app: setup
    spec:
      containers:
        - name: nexus
          image: sonatype/nexus3:latest
          env:
            - name: MAX_HEAP
              value: "2 GiB"
            - name: MIN_HEAP
              value: "1 GiB"
            - name: NEXUS_SECURITY_RANDOMPASSWORDS
              value: "false"
            - name: NEXUS_SECRETS_KEY_FILE
              value: /opt/sonatype/nexus/etc/nexus.secrets.json
          volumeMounts:
            - name: nexus-data
              mountPath: /nexus-data
            - name: nexus-config-volume
              mountPath: /opt/sonatype/nexus/etc/nexus.properties
              subPath: nexus.properties
            - name: nexus-secrets-volume
              mountPath: /opt/sonatype/nexus/etc/nexus.secrets.json
              subPath: nexus.secrets.json
          resources:
            requests:
              cpu: "4"
              memory: "4Gi"
            limits:
              memory: "4Gi"
              cpu: "4"
          ports:
            - containerPort: 8081
      volumes:
        - name: nexus-data
          persistentVolumeClaim:
            claimName: nexus-data-pvc
        - name: nexus-config-volume
          configMap:
            name: nexus-config
        - name: nexus-secrets-volume
          configMap:
            name: nexus-config

```
#### Recriando Recursos (Opcional)

Caso o Nexus já esteja rodando com configurações antigas, é possível deletar e aplicar novamente os recursos.

Deletando recursos existentes

```
kubectl delete deployment nexus -n nexus-3
kubectl delete service nexus -n nexus-3
kubectl delete configmap nexus-config -n nexus-3
kubectl delete pvc nexus-data-pvc -n nexus-3
```

Aplicando novamente os recursos

```
kubectl apply -f nexus-configmap.yaml -n nexus-3
kubectl apply -f nexus-pvc.yaml -n nexus-3
kubectl apply -f nexus-deployment.yaml -n nexus-3
kubectl apply -f nexus-service.yaml -n nexus-3
```

#### Verificação

Para garantir que tudo foi implantado corretamente:

```
kubectl get all -n nexus-3
```























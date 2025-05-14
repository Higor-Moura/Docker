# GERENCIAMENTO DE RECURSOS

## Especificando o uso **mínimo** de memória e CPU com `requests`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resources-pod
spec:
  containers:
  - name: apache-container
    image: httpd
    # Definição de recursos
    resources:
      # Definição de recursos mínimos (requests)
      requests:
        # cpu: 500m define que o container vai consumir metade de uma CPU
        cpu: "500m"
        # Definição de memória mínima
        memory: "128Mi"
```

---

## Especificando o uso **máximo** de memória e CPU com `limits`

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resources-pod
spec:
  containers:
  - name: apache-container
    image: httpd
    resources:
      requests:
        cpu: "500m"
        memory: "128Mi"
      # Definição de limites máximos de CPU e memória
      limits:
        cpu: "1000m"
        memory: "256Mi"
```

---

## Definindo `requests` e `limits` para dois ou mais containers

```yaml
apiVersion: v1
kind: Pod
metadata:
  name: resources-pod
spec:
  containers:
  - name: apache-container
    image: httpd
    resources:
      requests:
        cpu: "500m"
        memory: "128Mi"
      limits:
        cpu: "1000m"
        memory: "256Mi"

  - name: redis-container
    image: redis
    resources:
      requests:
        cpu: "400m"
        memory: "64Mi"
      limits:
        cpu: "500m"
        memory: "128Mi"
```

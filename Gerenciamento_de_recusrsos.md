# GERENCIAMENTO DE RECURSOS 

# Vamos criar um arquivo yml especificando o uso MINIMO de memoria e cpu de um container com o REQUESTS


```
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
# Definição de recursos minimos requests
      requests:
# cpu: 500m defini que o container vai consumir metade de uma cpu
        cpu: "500m"
# Definição de memoria 
        memory: "128Mi"
```

# Vamos criar um arquivo yml especificando o uso MAXIMO de memoria e cpu de um container com o LIMITS

```
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
# Definição de limite maximo de cpu e memoria 
      limits:
# Definição de uso maximo para 1 cpu
        cpu: "1000m"
        memory: "256Mi"
```
# Para Definir em dois ou mais containers 


```
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

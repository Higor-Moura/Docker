# Manifest File 

> - Agora que ja sabemos como subir um pod por comando.
> - Vamos aprender a subir um pod atraves do arquivo manifest files arquivo yml

#### Crie um arquivo manifest para executar o pod 

```
sudo vi pod_teste.yml
```

**arquivo manifest com a configuração do pod**

```
# versão da API
apiVersion: v1
# tipo do objeto que vamos criar, tipo do recurso 
kind: Pod
# metadados 
metadata:
# nome do recurso
  name: pod_webserver
# Etiquetas
  labels:
# Definindo etiquetas
    apps: my-app
    tier: frontend
# Especificações dos pods  
spec:
# definindo container
  containers:
# especificações do container
  - name: my-container-nginx
    image: nginx
```

#### Para subir o pod do manifest file use o comando 

```
kubectl create -f <nome do arquivo manifest.yml>
```
ou 

```
kubectl apply -f <nome do arquivo manifest.yml>
```
**pode ser usado se voce ja tiver subido o pod e quer alterar algo**

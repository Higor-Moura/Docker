# Manifest File 

> - Agora que ja sabemos como subir um pod por comando.
> - Vamos aprender a subir um pod atraves do arquivo manifest files arquivo yml

#### Crie um arquivo manifest para executar o pod 

```
sudo vi pod_teste.yml
```

**arquivo manifest com a configuração do pod**

```
apiVersion: v1
kind: Pod
  
metadata:
  name: pod_webserver
  labels:
    apps: my-app
    tier: frontend
    
spec:
  containers:
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

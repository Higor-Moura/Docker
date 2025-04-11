# COMANDOS KUBERNETES

#### Para visualizar PODs namespace padrão

```
kubectl get pods
```

**Para visualizar PODs de todos namespaces**

```
kubectl get pods --all-namespaces
```

**Para ter uma visualização mais completa dos PODs**

```
kubectl get pods -o wide
```

#### Para subir um pod 

```
kubectl run my-pod-aapache-server --image httpd
```

> - (kubectl run) = comando para executar
> - (my-pod-aapache-server) = nome do POD
> - (--image) = declara a imagem que vai subir
> - (httpd) = imagem do container que vai subir nesse caso o apache

#### Para deletar um POD de cada vez 

```
kubectl delete pods my-pod-aapache-server
```

> - `kubectl delete pods` =  comando para deletar o pod desejado
> - `my-pod-aapache-server` = nome do pod que vai ser deletado

**Para deletar todos os pods de uma vez**

```
kubectl delete --all pods
```

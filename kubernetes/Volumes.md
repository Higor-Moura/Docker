# VOLUMES

> - É um Diretor io onde os containers acessaram para guardar dados
> - Existem volumes `Efemeros` e `Persistentes`.

> - Volumes `Efemeros`: são dados, volumes temporários que só existem enquanto o pod estiver em execução. Quando o pod é deletado, reiniciado ou realocado para outro nó, o conteúdo do volume é perdido.

> - Volumes `Persistentes`  são recursos de armazenamento que garantem que os dados de um aplicativo continuem disponíveis, mesmo que o pod que os utiliza seja reiniciado ou removido.
 
```
apiVersion: v1
kind: Pod
metadata:
  name: redis-pod
spec:
  containers:
  - name: redis-container
    image: redis
    volumeMounts:
    - name: "cache-storage"
      mountPath: "/my-volume"

  volumes:
  - name: cache-storage
    emptyDir: {} 
```
No arquivo a cima estou usando o tipo de volume `emptyDir` ele é um volume efemero, mas ele consegue manter o arquivo intacto se o container sofrer reinicialização 

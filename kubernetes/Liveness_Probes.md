# LIVENESS PROBES

> - No Kubernetes são mecanismos que verificam se um contêiner está em um estado saudável e em execução.
> - Atraves do agente kubelete
> - O Liveness Probe toma uma ação quando o teste nao é bem sucedido, ou seja essa ação se traduz em reiniciar um determinado container

```
apiVersion: v1
kind: Pod
metadata:
  name: liveness-pod
spec:
  containers:
  - name: liveness-container-test
# imagem com diversas ferramentas com linha de comando
    image: busybox
# passando argumentos para este container 
    args:
# chamando o shell
    - /bin/sh
    - -c
# comandos que vai ser executado pelo sh
# criando o arquivo healthy esperando 30 segundo apaga o arquivo criado e espara 600 segundos  
    - touch /tmp/healthy; sleep 30; rm -f /tmp/healthy; sleep 600
    
    livenessProbe:
# executar 
      exec:
        command:
# ta dando um cat no arquivo criado 
        - cat
        - /tmp/healthy
# Atributos que devem ser respeitados
# ele vai esperar 5 segundos ante de executar o cat 
      initialDelaySeconds: 5
# a cada 5 segundo ele vai fazer a verificação
      periodSeconds: 5
# ele vai tentar 3 vezes executar o comando se caso nao der certo ele vai reiniciar o container 
      failureThreshold: 3
```

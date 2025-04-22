# DEPLOYMENTS

> - Faz a implantação da aplicação
> - `Rolling Updates (Rolling Release)` = executa uma atualização baseada em percentual de indisponibilidade de PODs por padrão é ter no maximo 25% de indisponibilidade do total de pods que voce tem rodando
> - EX: caso eu tiver quatro PODs associados a um Deployments a atualização sera feita de um por um. Ou seja no minimo eu terei 75% dos meus pods em status runing
> - `Recreate Deployment` = Mas pode causar indisponibilidade (Tem um risco associado). Ele vai parar todas as PODs e então vai subir todas as PODs com a versão nova da sua aplicação
> - `Rollback` = Se ouver algum problema em qualquer uma das estrategias voce pode fazer um Rollback e voltar ao estado que estava anteriormente


#### Crie o arquivo de configuração do Deployment

```
sudo vi deployment-teste.yml
```
**Conteudo do arquivo**

```
apiVersion: apps/v1
kind: Deployment
metadata:
  name: frontend-deployment
  labels:
    app: frontend

spec:
  template:
    metadata:
      name: pod-my-nginx
      labels:
        env: production
    spec:
      containers:
        - name: nginx-container
          image: nginx

  selector:
    matchLabels:
      env: production
  replicas: 4
```

#### Para executar o deployment

```
kubectl apply -f deployment-teste.yml
```

#### Verifique se o deployment funcionou

```
kubectl get deployment
```

**Quando subimos um deployment ele automaticamente sobe um replicaset junto, para verificar isso use o comando abaixo**

```
kubectl get replicaset
```


# DEPLOYMENT ROLLOUT

> - Um rollout é o processo de atualizar um Deployment com uma nova versão da aplicação. Pode ser uma nova imagem Docker, nova config, etc. O Kubernetes faz isso de forma controlada, garantindo que os pods antigos sejam substituídos sem downtime.

#### Ex:
>  Imagina que você tem um restaurante 🍔 e você quer trocar o cardápio antigo pelo novo, mas sem fechar o restaurante.

> Você faz assim:

> Coloca um novo garçom com o cardápio novo.

> Vê se ele tá trabalhando direitinho.

> Se tá tudo certo, manda embora um garçom velho com o cardápio antigo.

> Vai fazendo isso de pouquinho em pouquinho... até todos os garçons estão com o cardápio novo.

> Agora trocando os nomes:
> Restaurante = seu sistema no Kubernetes

> Garçom = um pod (parte do sistema que trabalha)

> Cardápio novo = nova versão do seu app

> Trocar garçons devagar = rollout

> Por que fazer assim?
> Porque se você troca todos os garçons de uma vez, e o novo cardápio tiver erro, todo mundo passa fome (ou seu sistema cai).


#### Para ver o status do Rollout

```
kubectl rollout status deployment.apps/frontend-deployment
```

> `kubectl rollout status` = Comando para ver o status
> `deployment.apps` = Aqui voce ta informando que é um deployment que voce quer ver
> `frontend-deployment` = Nome do deployment que voce subiu


#### Verificar dados do Deployment

```
kubectl describe deployment.apps/frontend-deployment
```

**Nos dados voce vai encontrar `RollingUpdateStrategy` ele vai mostrar a estrategia padrão de atualização do deployment**

**Voce vai verificar que vai ter `25% max unavailable` isso significa que no maximo 25% da aplicação vai ser atualizada por vez Ex: se tiver 4 PODs ele vai para 1 de cada vez**

**Ja o `25% max surge` ele é uma propria estrategia do update, ele cria sempre um POD a mais para garantir realmente que no maximo 1 POD vai estar indisponivel**

# Rollout History

> - É tipo um histórico de versões do seu app no Kubernetes.
Serve pra você saber o que mudou da ultima alteração e poder voltar no tempo se der ruim.

#### Comando para ver historico de versoes

```
kubectl rollout history deployment.apps/frontend-deployment
```

> - `kubectl rollout history` = Comando para ver historico
> - `deployment.apps` = Especifica que é de deployment
> - `frontend-deployment` = Nome do deployment

**SE QUISER ANALISAR DADOS DE UMA VERSÃO ESPECIFICAR**

```
kubectl rollout history deployment.apps/frontend-deployment --revision=2
```
> - `--revision=2` = Especifica o numero da versão que deseja voltar 
 
# DEPLOYMENT ROLLBACK

> - É a possibilidade de voltar para uma versão anterio se caso algo der errado

#### Comando para fazer rollback para uma versão anterior 

```
kubectl rollout undo deployment.apps/frontend-deployment
```
#### Comando para fazer rollback para uma versão especifica 

```
kubectl rollout undo deployment.apps/frontend-deployment --to-revision=5
```

# ROLLOUT PAUSE & RESUME

#### Comando para pausar a atualização

```
kubectl rollout pause deployment.apps/frontend-deployment
```

#### Comando Para retomar a atualização 

```
kubectl rollout resume deployment.apps/frontend-deployment
```
# DEPLOYMENT SCALE UP & DOWN

```
kubectl scale deployment.apps/frontend-deployment --replicas=11
```

> - `--replicas=11` =  Especifica a quantidade que deseja tanto aumentar ou diminuir 









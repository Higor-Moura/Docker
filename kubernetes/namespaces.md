# NAMESPACES

> - Utilizado para fazer uma organização logica dentro do cluster
> - Mecanismo utilizado para isolar os grupos de recursos dentro de um unico cluster

#### O que pode ser colocado dentro de um namespaces

> - Os objetos que podem ser colocados dentro de um namespaces são `namespace-based scoping` (Ex: Pods, Deployment etc.)

**OBS: todo objeto criado tanto por comando ou arquivo yaml por padrão e direcionado para o namespace `default`**

**SE CASO QUEIRA MUDAR ISSO USE O COMANDO A BAIXO**

```
kubectl config set-context --current --namespace=<nome do namespace que deseja>
```

#### O que não pode ser colocado dentro de um namespaces

> - Os objetos que não podem ser colocados dentro de um namespace são `cluster-wide objects` (Ex: Nodes,Persistent Volumes etc.)

#### Comando para cria um namespace

```
kubectl create namespace frontend --save-config
```

> - `kubectl create namespace` = comando para criar namespace
> - `frontend` = nome do namespace que estou criando
> - `--save-config` =  tag para fazer essa criação

#### Para visualizar os namespace 

```
kubectl get ns 
```

**CUIDADO AO EXCLUIR UM NAMESPACE QUANDO EXCLUIDO, TODOS OS RECURSOS DENTRO DESSE NAMESPACE TAMBEM SÃO EXCLUIDOS !**

#### Comando para deletar namespace

```
kubectl delete namespace frontend
```

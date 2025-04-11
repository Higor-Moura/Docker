# KUBERNETES FUNDAMENTOS E CONCEITOS

> O Kubernetes executa verificações de integridade continuamente nos seus serviços, reiniciando os contêineres que falharam ou pararam e só disponibilizando os serviços aos usuários quando confirma que eles estão em execução.
> Um Administrador/Orquestrador de container
****
## DISPONIBILIDADE KUBERNETES

#### SELF-HEALING SYSTEM

> - **Sistema de auto correção Ex: imagine que voce tenha um problema na aplicação, o kubernetes te da opções e recursos principalmente automatizados para que o sistema consiga se levantar desse  problema que houve durante seu funcionamento, sistema de auto correção**

#### AUTOSCALE UP/DOWN

> - **Enfatiza a questão da disponibilidade, ele mantem o estado desejado automaticamente**

#### DEVOPS AUTOMATION TOOL

> - **Automação de tudo que pode ser automatizado para evitar erros humanos**

#### FAULT PROTECTION

> - **Ações preventivas contra a indisponibilidade**

# CLUSTER

**Cluster é tudo que esta dentro do tracejado vermelho**
**Cluster é um conjunto de maquinas vinculadas, para se indentificar como uma só.**
**EX: pego 3 vms e crio um cluster das 3, no caso se uma desligar ou cair as outras duas vão manter as aplicações rodando**

![Captura de tela de 2025-04-04 12-01-56](https://github.com/user-attachments/assets/dfb2cbc1-9e35-465d-b425-23ac5ff579c6)

# CONTROL PLANE

## etcd

> - **etcd é o mais importante, ele é o banco de dados do kubernetes uma database do tipo chave valor**

## API-server

> - api server faz o controle de tudo, tudo passa pela API.
> - O Kubernetes nada mais é do que uma api, quando voce executa `kubectl get pods` voce ta rodando uma requisição do tipo HTTP do tipo get para a API do kubernetes que é o API-server.

## SCHED

> - O sched decide em qual NODE vai colocar um determinado POD
> - Voce cria um POD ele vai para o estado de peding ate o sched analisar os recursos e escolher o melhor node para adicionar o pode

## c-m (controller manager)

> - É um conceito que ele fica analisando algo para tomar uma ação
> - Então eles pegaram varios controles do kubernetes compilaram dentro do controller meneger e colocaram ali
> - EX: quando criamos um job ele pega desmenbra e cria um POD baseado naquelas especificações

# DATA PLANE

## NODE

> - Node do dataplane são VMs ou maquinas fisicas, onde vai rodar a aplicação
> - EX: para melhor entendimento pense que o node é um navio e o kubelet é o capitão do navio

#### kubelet

> - Ele se conecta diretamente com o API-server do control-plane
> - Quando voce que acessar um pod que esta dentro de um node, voce fala com o api-server, o api-server fala com kubelet rodando naquele node e então envia os comandos
> - Kubelet é meio que uma ponte entre o control-plane e o node

#### k-proxy

> - K-proxy ele é um container que ja vem pré-instalado quando fazemos um deploy de um cluster
> - Ele faz algo bem especifico que é criar o service
>   `service` é um IP virtual que vai fazer um balanciamento de carga dos podes isso é feito por default por via regras de iptables no node
>   Então quando voce  cria um service o K-proxy vai la no node e cria todas as regras de ip-tables que ta rodando naquele node


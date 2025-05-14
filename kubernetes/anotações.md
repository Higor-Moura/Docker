
# KUBERNETES FUNDAMENTOS E CONCEITOS

> O Kubernetes executa verificações de integridade continuamente nos seus serviços, reiniciando os contêineres que falharam ou pararam e só disponibilizando os serviços aos usuários quando confirma que eles estão em execução.
> Um Administrador/Orquestrador de container

****

## DISPONIBILIDADE KUBERNETES

### SELF-HEALING SYSTEM

- Sistema de auto correção. Ex: imagine que você tenha um problema na aplicação, o Kubernetes te dá opções e recursos — principalmente automatizados — para que o sistema consiga se recuperar desse problema ocorrido durante seu funcionamento.

### AUTOSCALE UP/DOWN

- Enfatiza a questão da disponibilidade. Ele mantém o estado desejado automaticamente.

### DEVOPS AUTOMATION TOOL

- Automação de tudo que pode ser automatizado para evitar erros humanos.

### FAULT PROTECTION

- Ações preventivas contra a indisponibilidade.

# CLUSTER

Cluster é tudo que está dentro do tracejado vermelho.  
Cluster é um conjunto de máquinas vinculadas para se identificar como uma só.  
Exemplo: pego 3 VMs e crio um cluster com as 3. Se uma desligar ou cair, as outras duas vão manter as aplicações rodando.

![Cluster](https://github.com/user-attachments/assets/dfb2cbc1-9e35-465d-b425-23ac5ff579c6)

# CONTROL PLANE

## etcd

- O `etcd` é o mais importante: ele é o banco de dados do Kubernetes — uma database do tipo chave-valor.

## API-server

- O API Server faz o controle de tudo. Tudo passa pela API.
- O Kubernetes nada mais é do que uma API. Quando você executa `kubectl get pods`, você está rodando uma requisição HTTP do tipo GET para a API do Kubernetes, que é o API Server.

## Scheduler (SCHED)

- O Scheduler decide em qual Node vai colocar um determinado Pod.
- Você cria um Pod, ele vai para o estado de *Pending* até o Scheduler analisar os recursos e escolher o melhor node para adicionar o Pod.

## Controller Manager (c-m)

- Ele fica analisando algo para tomar uma ação.
- Reúne vários controladores do Kubernetes em um só lugar.
- Exemplo: quando criamos um Job, ele desmembra e cria um Pod baseado naquelas especificações.

# DATA PLANE

## Node

- Nodes do Data Plane são VMs ou máquinas físicas onde vai rodar a aplicação.
- Exemplo: pense que o Node é um navio e o Kubelet é o capitão do navio.

### Kubelet

- Se conecta diretamente com o API Server do Control Plane.
- Quando você acessa um Pod dentro de um Node, você fala com o API Server, que se comunica com o Kubelet naquele Node para enviar os comandos.
- O Kubelet é uma ponte entre o Control Plane e o Node.

### Kube-proxy

- O `kube-proxy` é um container que já vem pré-instalado ao criar um cluster.
- Ele é responsável por criar o `Service` — um IP virtual que faz o balanceamento de carga dos Pods.
- Isso é feito via regras de `iptables` no Node.
- Quando você cria um `Service`, o `kube-proxy` atualiza as regras de rede nos Nodes para rotear o tráfego adequadamente.

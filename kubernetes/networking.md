# KUBERNETS NETWORKING

 #### TIPOS DE REDE KUBERNETES

**Container to Container Communication**

> - Um ou mais container dentro de um Pod compartilha o mesmo hostnetwork
> - Nesse caso os Pods terão seus proprios endereço ip (todos os containers compartilham o mesmo endereço ip). Mas funcionam em uma porta diferente
> - A comunicação entre os containers acontece dentro do proprio Pod, porem em uma porta diferente

**Pod to Pod Communication**
> - `Intra Node Pod Network` É a comunicação de Pods rodando em um single node nessse caso todos os endereços IPs do pods serão diferentes e atribuidos atraves da sua rede local pois compartilham o mesmo host
> - `Endereços IP`  

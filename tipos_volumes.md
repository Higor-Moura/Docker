# TIPOS DE MOUNT

**BIND,NAMED E DOCKERFILE VOLUME**

## BIND 

As montagens Bind são basicamente apenas vincular um determinado diretorio ou arquivo do host dentro do container:

```bash
docker run -v /hostdir:/containerdir mysql
```

> **ℹ️ Informação:**
>  - `-v` Volume
>  - `/hostdir` voce vai alterar pelo diretorio do host onde quer salvar os dados do container
>  - `/containerdir` diretorio do container onde é salvo as coisas
>  - `mysql` imagem a ser baixada

## NAMED

Volumes nomeados são volumes que voce cria manualmente com o comando:

```bash
docker volume create <nome-do-volume>
```

Eles são criados em /var/lib/docker/ volumes e podem ser referenciados apenas por seu nome.

Digamos que voce crie um volume chamado "mysql_data", voce pode apenas referencialo com o comando:

```
docker run -v mysql_data:/containerdir mysql
```

## DOCKERFILE

Tipo de volume que são criados pela instrução VOLUME. Esses volumes 
tambem são craidos em /var/lib/docker/ volumes, mas não tem um
determinado nome. O volume é criado ao executar o container e são uteis
para salvar dados persistentes. O desenvolvedor pode dizer onde estão os 
dados importantes e o que deve ser persistente.


## QUAL DEVO UTILIZAR ?

Depende de voce. Se voce quiser manter tudo na "area do docker"(/var/lib/docker),voce pode usar volumes. 
Se voce deseja manter sua propria estrutura de diretorio, voce pode usar binds.

**O Docker recomenda o uso de volumes em vez do uso de binds, pois os volumes são criados e gerenciados pelo docker.**



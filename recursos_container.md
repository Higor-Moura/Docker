# LIMITANDO MEMORIA E CPU

#### Verifique a quantidade de recursos que estão sendo utilizados pelo container.

```bash
docker stasts <nome do container> 
```

#### Para limitar os recursos de um container ja criado 

```bash
docker update <nome do container> -m 128m --cpus 0.2
```
> **ℹ️ Informação:**
> - `-m` memoria `128m` quantidade que eu quero limitar a memmoria do container
> - `--cpus` limite de processamento para o container

**SE DER ERRRO**
> Memory limit should be smaller than already set memoryswap limit, update the memoryswap at the same time
> Use o comando a seguir para aumentar a memoria swap

```bash
docker update --memory-swap 1024M --memory 1024M <nome do container>
```
**FEITO ISSO PODE RODAR O COMANDO PARA LIMITAR A MEMORIA**

## TESTE PARA SABER SE DEU CERTO 

> Abra dois terminais no container!
> Em um terminal voce vai rodar o stats para analisar o consumo do container
> E no outro terminal voce vai estressar o container para ver se realmente esta limitando a quantidade que foi especificada

**Terminal 1**

```bash
docker stats <nome do container>
```

> vai aparecer uma imagem como essa:

![Captura de tela de 2025-03-25 08-55-10](https://github.com/user-attachments/assets/9241b0b4-47a7-4bce-8b1f-f22b2a3bd216)


> feito isso vá para o proximo terminal do mesmo container.

**Terminal 2**

#### execute o comando para entrar no terminal do container 

```bash
docker exec -ti <nome do container> bash
```
#### Atualize os pacotes do container 

```bahs
apt update
```

#### Instale o comando Stress para testar os recursos 

```bash 
apt -y install stress
```

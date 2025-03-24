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

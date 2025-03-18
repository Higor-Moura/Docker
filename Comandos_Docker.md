# Comandos Docker 

#### 1. Comando para ver quantos conteiners e quais conteiners estão executando na maquina.

```
docker ps
```
ou
```
docker container ls
```
> **ℹ️ Informação:** 
> - Esse comando mostrará conteiners que tenha processo rodando! quando o conteiner nao tem processo rodando ele é finalizado.
> - O conteiner so continuará executando caso tenha algum processo rodando nele.

#### 1.1 Caso queira ver todos os conteiners mesmo os que ja pararam de executar use o comando a baixo.

```
docker ps -a
```
ou
```
docker container ls -a
```
#### 2. Comando para criar ou executar um conteiner, no exemplo abaixo vou criar um com ubuntu.

```
Docker run ubuntu
```
> - Porem como nao tem nenhum processo executando nele, ele nao aparecera no `docker ps`.
> - Para fazer com que ele apareca la vamos abrir um terminal nele para ter um processo rodando.

#### Para abrir um terminal no conteiner do ubuntu use o comando abaixo.

```bash
docker run -it ubuntu bash
```
**Explicação:**

-  `-it`: `i` Modo interativo `t` utiliza o tty para  permitir interação com o terminal.
-  `bash`: Inicia o shell Bash dentro do contêiner.

#### Para executar um comando dentro do conteiner 

```bash
docker exec -iti <id do conteiner> bash
```

#### Para parar os processos do conteiner.

```bash
docker stop <id do conteiner>
```

#### Para iniciar o conteiner.

```bash
docker start <id do conteiner>
```

#### Para nomear um container 

```bash
docker run -dti --name <nome que voce quer> <imagem do container> 
```
> **ℹ️ Exemplo:** 
> - `docker run -dti --name ubuntu-A ubuntu ` 

# COPIA

#### Copiar arquivo da maquina fisica para container

```bash
docker cp <nome do arquivo> <nome do container destino>:<caminho de destino>
```

> **ℹ️ Exemplo:** 
> - `docker cp teste.txt ubuntu-A:/home` 

#### Copiar arquivo do container para maquina fisica

```bash
docker cp <nome do container origem>:<origem do arquivo> <caminho de destino>
```

> **ℹ️ Exemplo:** 
> - `docker cp ubuntu-A:/home/teste.txt /home/higor/virustrojan.txt` 

# TAG

> Uma tag Docker é um rótulo que aponta para uma imagem específica dentro de um repositório. Por padrão, o Docker usa a tag latest se nenhuma tag for especificada.

**Ex: abaixo um exemplo do debian para baixar a versão 9**

```bash
docker pull debian:9
```










# Comandos Docker 

#### 1. Comando para ver quantos conteiners e quais conteiners estão executando na maquina.

```
docker ps
```
> Esse comando mostrará conteiners que tenha processo rodando! quando o conteiner nao tem processo rodando ele é finalizado.
> O conteiner so continuará executando caso tenha algum processo rodando nele.

#### 1.1 Caso queira ver todos os conteiners mesmo os que ja pararam de executar use o comando a baixo.

```
docker ps -a
```
#### 2. Comando para criar ou executar um conteiner, no exemplo abaixo vou criar um com ubuntu.

```
Docker run ubuntu
```
> Porem como nao tem nenhum processo executando nele, ele nao aparecera no `docker ps`.
> Para fazer com que ele apareca la vamos abrir um terminal nele para ter um processo rodando.

#### Para abrir um terminal no conteiner do ubuntu use o comando abaixo.

```bash
#O "-it" é para interagir é de interativo, e o "bash" é para abrir o terminal
docker run -it ubuntu bash
```

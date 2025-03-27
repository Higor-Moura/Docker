# DOCKER COMPOSE

> Para teste irei usar o docker compose para subir um container mysql e um container com adminer

#### Para iniciar vamos preparar o ambiente no host Docker

**Crie os diretorios para organização**

```bash
cd /data
sudo mkdir banco
cd /
sudo mkdir compose
cd compose/
sudo mkdir primeiro
cd primeiro/
```

#### Crie o arquivo docker-compose.yml

```bash
sudo vi docker-compose.yml
```
> Configuração do arquivo

```bash
# versão do yaml
version: '3.8'
# Services especifica qual serviço vai ser instalado
services:
# Nome do primeiro serviço
  mysqlsrv:
# Imagem do serviço
    image: mysql:5.7
# variavel de ambiente
    environment:
      MYSQL_ROOT_PASSWORD: "Senha123"
      MYSQL_DATABASE: "testedb"
# Portas
    ports:
      - "3306:3306"
# Volumes onde é feito o backup do container no host,
# O primeiro caminho é do host onde deseja salvar os dados do banco no host
# Depois do ":" é o caminho do container onde é salvo os dados 
    volumes:
      - /data/banco:/var/lib/mysql
# criando uma rede chamada "minha-rede"
    networks:
      - minha-rede
# adminer ja é outro services 
  adminer:
# imagem do adminer 
    image: adminer
# porta que vai ser usada pelo adminer no host e no container
    ports:
      - 8083:8080
# colocando ele na mesma rede para conversar com o container mysql
    networks:
      - minha-rede
# criei uma rede chamada "minha-rede" e o driver da rede sera o modo "bridge" para criar comunicação do container com o host
networks:
  minha-rede:
    driver: bridge
```
> Observe que vai ser criado dois containers, um do mysql e o outro do adminer.

#### Use o docker-compose para subir os containers

> Ele ja sabe qual é o arquivo e a opção `-d` é para rodar em segundo plano.
```bash
docker-compose -d 
```
#### Verifique se subiu os containers 

```bash
docker ps
```
> - **Acesse o adminer via web passando o ip do host e a porta liberada no arquivo compose**
> - Ex: 10.0.0.189:8083
> - os dados para login esta no arquivo docker-compose

#### Para parar os containers 

```
docker-compose down
```
**Ele ira para os containers criado pelo compose e excluira a rede criada no arquivo**

# DOCKER FILE

> **Usarei como exemplo uma aplicação python onde pede o nome do usuario e depois devolve o nome ao usuario**
> - Um Dockerfile é um arquivo de texto que contém instruções para criar uma imagem de contêiner.
> - É uma espécie de receita que guia a criação de uma imagem personalizada para as suas necessidades.

#### Crie uma estrutura de Diretorios, para imagens no host docker.

```bash
sudo mkdir /images
cd /images
sudo mkdir /ubuntu-python
cd /ubuntu-python
```
#### Crie um arquivo com a aplicação python

```bash
sudo vi app.py 
```
> conteudo do arquivo

```
nome= input("Qual e o seu nome?:")
print (nome)
```
 
#### Crie o arquivo dockerfile

```bash
sudo vi dockerfile
```
> conteudo do arquivo
```bash
# Indicar a imagem que eu quero subir o container.
# Se quiser especificar versão so adicionar a tag ":"

FROM ubuntu

# O que vai ser executado dentro desse ubuntu
# Dois && para inserir o proximo comando 

RUN apt update && apt install -y python3 && apt clean

# Copiar o arquivo app.py que esta aqui no host para o container 
 
COPY app.py /opt/app.py

# Executar a aplicação

CMD python3 /opt/app.py
```

**COMANDOS DOCKERFILE**
> `FROM` Indica a base do container
> `RUN`  O que vai executar no container 
> `COPY` O que vai copiar
> `CMD`  Para executar os comandos do bash

#### Para buildar o dockerfile 

```bash
docker build <caminho do docker file> -t <o nome que deseja para imagem>
```

#### Para executar a imagem 

```bash
docker run -ti --name <nome da imagem> <imagem que voce criou no comando a cima >
```


# DOCKEFILE APACHE

#### No Diretorio `/images` no host Docker crie um diretorio para o apache

```bash
sudo mkdir ubuntu-wiki
cd ubuntu-wiki/
```

#### baixe uma imagem de alguma aplicação web .tar:

> No meu caso vou usar o mediawiki

```bash
wget https://releases.wikimedia.org/mediawiki/1.43/mediawiki-1.43.0.tar.gz
```

#### Crie o arquivo dockerfile

```bash
sudo vi dockerfile
```
> Configuração do arquivo

```bash
# FROM indica o sistema que eu quero subir o container.
# Se quiser especificar versão so adicionar a tag ":" logo depois a versão

FROM ubuntu

# RUN indica o que vai ser executado dentro desse ubuntu
# Dois "&&" para inserir o proximo comando 

RUN apt-get update && apt-get install -y apache2 && apt-get clean && apt-get install -y php php-intl php-mbstring php-apcu php-curl php-mysql php-xml
# No caso do apache é preciso configurar algumas variaveis do sistema 

# Para evitar que tenha mais de uma execução do apache no mesmo container
ENV APACHE_LOCK_DIR="var/lock"
# Especificação do arquivo tipo pid é um arquivo que contem o numero de identificação do processo (pid)
ENV APACHE_PID_FILE="var/run/apache2.pid"
# Especificar o usuario que vai executar o apache
ENV APACHE_RUN_USER="www-data"
# Especificar o grupo do usuario
ENV APACHE_RUN_GROUP="www-data"
# Especificar o diretorio de log
ENV APACHE_LOG_DIR="/var/log/apache2"

# ADD aqui é adicionado a imagem que foi baixada com o wget, o ADD envia o arquivo para o local especificado e descompacta 
ADD mediawiki-1.43.0.tar.gz /var/www/html

# Especifica a descrição
LABEL description = "Apache webserver"

# Especifica onde os dados serão salvos dentro do container 
VOLUME /var/www/html

# Especifica a porta do container que vai expor 
EXPOSE 80

# Especificar qual aplicação vai utilizar, como vai ser uma aplicação executada em primeiro plano usarei o ENTRYPOINT para executar o arquivo do apache
ENTRYPOINT ["/usr/sbin/apachectl"]

# Indicar que o arquivo deve ser executado em primeiro plano
CMD ["-D","FOREGROUND"]
```

#### Com o dockerfile pronto vamos gerar a imagem

```bash
docker image build -t ubuntu-wiki .
```
**Explicação**
> `-t` especifica o nome da imagem
> `.` caminho do dockerfile como ja estou no diretorio do docker file usei o ponto

#### Vamos subir a imagem

```bash
docker run -dti -p 80:80 --name wiki ubuntu-wiki
```
**Explicação**
> - `80:80` a primeira opção é a porta do host, ja a segunda é a porta do container que foi declarada no dockerfile

#### so acessar a pagina web passando o ip da maquina o nome do diretorio criado pelo arquivo tar e o index.php

```
<ip do host>:8082/mediawiki-1.43.0/mw-config/index.php
```

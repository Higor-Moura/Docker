# COMO UTILIZAR MOUNT

> É uma forma de dar acesso ao containers a arquivos e pastas do host.
> Utilazado para nao perder dados caso o container caia.
> Antes de tudo temos que ver onde o container salva o banco de dados

#### Para verificar onde os dados são salvos dentro do container.

```bash
docker inspect <nome do container>
```

> Vai aparecer varias informações do sistema, procure a parte `Mounts`:

![Captura de tela de 2025-03-21 08-51-51](https://github.com/user-attachments/assets/03731ace-9bab-4b40-b892-7bc1b7694ff5)

> Dentro de Mounts tem o Destination com o caminho, como esta destacado na imagem, esse é o caminho onde são salvo os dados

> - O que vamos fazer é dizer para o container que tudo que for salvo nesse caminho.
> - Sera direcionado para fora do container, ou seja no host.

#### Crie um diretorio no `/` do host com o nome `data` e dentro do diretorio data crie outro diretorio com o nome do container no meu caso é `mysql`:

```bash
mkdir /data
mkdir /data/mysql
```
#### Pare o container 

```bash
docker stop mysql
```

#### Remova o container 

```bash
docker rm mysql
```

#### Agora suba um container montando o volume especificando o caminho do diretorio que foi criado 

```bash
docker run -e MYSQL_ROOT_PASSWORD=1234 -e MYSQL_DATABASE=testeDB --name mysql -d -p 3306:3306 --volume=/data/mysql:/var/lib/mysql mysql
```
> **ℹ️ Informação:** 
> - `-e` Declarar variavel de ambiente
> - `--name` Especificar nome do container
> - `-d` Rodar em background
> - `-p` Especificar porta
> - `--volume` Montar o volume para nao perder os dados caso o container caia
> - Por ultimo `mysql` imagem que vai subir

#### Logar no usuario ROOT do banco

```bash
mysql -u root -p --protocol=tcp
```

#### Para visualizar as bases disponiveis 

```bash
show databases;
```
> Vai verificar que a base de dados especificado no comando a cima estara criada.

#### Agora de um ls no diretorio criado anteriormente `/data/mysql`

```bash
ls /data/mysql/
```
> vai identificar que foi criado varios arquivos!

#### Vamos testar se deu certo parando e excluindo o container 

```bash
docker stop mysql
```
```bash
docker rm mysql
```
####  Vamos subir outro container mas dessa vez sem a variavel de database para ver se ela vai puxar do outro container  

```bash
docker run -e MYSQL_ROOT_PASSWORD=1234 --name mysql -d -p 3306:3306 --volume=/data/mysql:/var/lib/mysql mysql
```

#### Logar no usuario ROOT do banco

```bash
mysql -u root -p --protocol=tcp
```

#### Para visualizar as bases se foi puxada a do outro container  

```bash
show databases;
```

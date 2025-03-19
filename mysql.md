# Create container mysql

**Baixar a imagem do banco**

```bash
docker pull mysql
```
#### Para executar a imagem setando variaveis de ambiente use a opção `-e`

```bash
docker run -e MYSQL_ROOT_PASSWORD=SENHA --name mysql -d -p 3306:3306 mysql
```
#### Acesse o terminal do container para fazer a configuração do banco 

```bash
docker exec -it mysql bash
```

#### Logar no usuario ROOT do banco para cria uma base de dados 

```bash
mysql -u root -p --protocol=tcp
```

#### Criar database 

```bash
CREATE DATABASE <NOME DA BASE>;
```

#### Para visualizar as bases disponiveis 

```bash
show databases;
```

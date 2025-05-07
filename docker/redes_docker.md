# REDES

**Para visualizar o IP do docker e o tipo de rede, no host cole o comando**

```bash
ip -c a
```

![Captura de tela de 2025-03-25 10-07-21](https://github.com/user-attachments/assets/d62b5287-da07-4332-83af-e993c87b36a5)

#### Para visualizar as redes disponiveis 

```
docker network ls
```

![Captura de tela de 2025-03-25 10-08-29](https://github.com/user-attachments/assets/99c4f93d-c02f-4808-b6c0-455d82cf1670)

# TIPOS DE REDES

### Bridge

> Todo container criado é adicionado por padrão nessa rede Bridge,
> que tem acesso ao Host, ou seja, consegue se comunicar com o Host.
> por isso sempre que indica o ip do host, é possivel ter acesso aos containers

> **ℹ️ Exemplo:**
**Utilize o comando**

```bash
docker network inspect bridge
```
> vai observar que ira aparecer os conteiners qeu estão adicionados a essa rede.
> se voce nao especificar a rede ao criar o container. Todo container criado ira para essa rede.
> por tanto todos os containers se comunicam por estar na mesma rede.

### Host

> host é a rede padrão 

### None

```
```
### Para isolar um container, ou um grupo de containers. Pode ser criado uma rede e colocar os containers que deseja isolar nessa rede.

#### Para criar uma nova rede

```bash
docker network create <nome que desja para rede>
```

#### Crie um container agora especificando a rede

```bash
docker run -dti --name <nome do container> --network <nome da rede qeu voce criou> mysql
```
> **ℹ️ Informação:**
>  `mysql` no final do comando é a imagem que eu estou usando como exemplo para criar o container

#### Para verificar se foi criado na rede certa

```bash 
docker network inspect <nome da rede qeu voce criou>
```
> Para fazer o teste de cominucação pode criar outro container na mesma rede e ver se um consegue pingar o outro 

#### Crie outro container especificando a mesma rede

```bash
docker run -dti --name <nome do container> --network <nome da rede qeu voce criou> mysql
```
> Agora é so executar um ping de um container para o outro para realizar o teste!
> E testa o ping desse container para um que nao esta na mesma rede.

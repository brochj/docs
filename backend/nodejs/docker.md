# Docker  <!-- omit in toc --> 
- [Instalando o Docker](#instalando-o-docker)
- [Comandos básicos](#comandos-b%c3%a1sicos)
- [Criando o container](#criando-o-container)
- [Postbird GUI](#postbird-gui)
  - [Criando o Database](#criando-o-database)


## Instalando o Docker
- Pesquisar por [**docker ce**](https://docs.docker.com/install/linux/docker-ce/ubuntu/) e seguir os passos de instalação.

- Depois de instalado, realizar o [postinstall](https://docs.docker.com/install/linux/linux-postinstall/) para evitar usar `sudo` toda hora que for utilizar o comando `docker`. (requer um reboot da máquina para aplicar as mudanças).
  
- No Postinstall não configurar para start on boot.

- Rodar `docker -v` e `docker run hello-world` para ver se está tudo certo.

## Comandos básicos

| Comando | Descrição | 
|:-------|:-------------------|  
|`docker ps` | Lista os containers ativos |
|`docker ps -a` | Lista os containers criados |
|`docker stop <container-name>`| Para de executar um container|
|`docker start <container-name>`| Começa a executar um container|
|`docker logs <container-name>`| Ver log do container (util pra quando der erro)|



## Criando o container
- Pesquisar por [docker postgres](https://hub.docker.com/_/postgres) lá terá como utilizar a imagem

`$ docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres`

> O username padrão é `postgres` (pode ser alterado)


- Exemplo
```bash
  docker run --name meetappDB -e POSTGRES_PASSWORD=docker -p 5432:5432 -d postgres
```
- `-d` nome da imagem do Docker Hub 

- `-p` redirecionamento de portas 
```bash
-p portaDoPC:portaDoContainer
```

## Postbird GUI
Postbird é GUI para Postgres

- Instalar utilizando o .deb do [site oficial - electronjs.org](https://electronjs.org/apps/postbird) ou instalar via snap [postbird - github](https://github.com/Paxa/postbird)
```bash
sudo snap install postbird
```

- Colocar os dados de username e password de acordo com o foi feito no docker e dar um `test connection` para ver se está tudo OK.

- Salvar e conectar.

### Criando o Database
- No menu lateral `select database`, dar um `create database` e **definir um nome** (template vazio e encoding UTF8(client encoding)).

> IMPORTANTE: O nome da database (aqui no Postbird) terá que ser o mesmo que será criado no arquivo `config/database`  se não vai dar o erro abaixo quando for executar a migration lá na frente.

- **Exemplo**
- Se no arquivo `database/config.js` o nome database for `meetapp`.
```js
  module.exports = {
    ...
    database: 'meetapp',
    ...
  };
```

- E nome do database no Postbird for `meetappsss` vai dar o seguinte erro quando for executar a migration.
```bash
Loaded configuration file "src/config/database.js".
ERROR: database "meetappsss" does not exist
error Command failed with exit code 1.
``` 


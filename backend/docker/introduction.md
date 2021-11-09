# Comandos relacionados à informações

- o `docker version` - exibe a versão do docker que está instalada.
- o `docker inspect ID_CONTAINER` - retorna diversas informações sobre o container.
- o `docker ps` - exibe todos os containers em execução no momento.
- o `docker ps -a` - exibe todos os containers, independente de estarem em execução ou não.

# Comandos relacionados à remoção

- o `docker rm ID_CONTAINER` - remove o container com id em questão.
- o `docker container prune` - remove todos os containers que estão parados.
- o `docker rmi NOME_DA_IMAGEM` - remove a imagem passada como parâmetro.

# Docker Create

```
docker create [options] IMAGE
  -a, --attach               # attach stdout/err
  -i, --interactive          # attach stdin (interactive)
  -t, --tty                  # pseudo-tty
      --name NAME            # name your image
  -p, --publish 5000:5000    # port map
      --expose 5432          # expose a port to linked containers
  -P, --publish-all          # publish all ports
      --link container:alias # linking
  -v, --volume `pwd`:/app    # mount (absolute paths needed)
  -e, --env NAME=hello       # env vars
```

## Inspecting The Container

List all images that are locally stored with
the Docker Engine

`docker image ls`

# Run

Run a container from the Alpine version 3.9 image, name the running container “web” and expose port 5000 externally, mapped to port 80 inside the container.

`docker container run --name web -p 5000:80 alpine:3.9`

# Usando Volumes para rodar código dentro de container

Volumes são pastas dentro do container que estão "linkadas" com um pasta fora do container. Isso é interessante pois posso salvar dados e depois excluir o container.

```shell
# sintaxe
docker run -d -p <porta-host>:<porta-container> -v "<pasta-fora-do-container>:<pasta-dentro-do-container>" -w "<pasta-dentro-do-container>" <imagem> <comando simples>

docker run -d -p 8080:3000 -v "/pj/meu-dados:/var/www" -w "/var/www" node npm start

```

flag `-d` é para executar o `detach`, para não ficar com o terminal "ocupado" pela aplicação
flag `-v` é pro volume
flag `-w` é 'working directory', ou seja, a pasta onde vai ser executado o comando simples

# Construir as próprias imagens

Tem que criar um arquivo chamado `Dockerfile` na pasta raiz do projeto (pode ser `Dockerfile` sem extesão mesmo, ou `node.dockerfile`)

### Exemplo para um site estático com node

```dockerfile
FROM node:latest
MAINTAINER Broch
ENV NODE_ENV=production
ENV PORT=3000
COPY . /var/www
WORKDIR /var/www
RUN npm install
ENTRYPOINT npm start
EXPOSE $PORT
```

- `ENV NODE_ENV=production` pode criar quantas variáveis de ambiente você quiser

- `COPY . /var/www` copia toda a pasta do projeto para dentro `/var/www`

- `WORKDIR /var/www` mudar de diretório

- `EXPOSE 3000` porta dentro container

Agora vamos buildar a imagem utilizando o `dockerfile`

```sh
docker build -f <arquivo-dockerfile> -t <nome-da-imagem> <pasta-onde-esta-projeto>

docker build -f Dockerfile -t brock/node .
```

Depois dar um `docker images` para ver a imagem criada

Depois para ver se o container ta funcionando

```sh
docker run -d -p 8080:3000 brock/node
```

# Subir Imagem para DockerHUB ou DockerStore

1. Criar uma conta no DockerHUB

2. Logar no terminal com `docker login`

3. `docker push <nome-da-imagem>`

Agora você consegue compartilhar com outras pessoas essa imagem, ou você mesmo utilizar ela em outros dispositivos rodando o comando

`docker pull <nome-da-imagem>`

# Comunicação entre Containers

Por padrão o docker cria uma rede interna (default network), onde todos os conteineres estão nela, e cada container possui um ip na rede.

Mas usando a rede interna padrão não temos controle do número de ip,

Então vamos criar a nossa própria rede

```sh
docker network create --driver bridge minha-rede

```

```sh
docker network ls
```

Agora com a rede criada, vamos rodar um container utilizando a nossa rede

```sh
docker run -it --name meu-container --network minha-rede ubuntu
```

Para verificar a network do container

```sh
docker inspect meu-container
```

Agora vamos subir outro container nessa mesma rede

```sh
docker run -it --name meu-segundo-container --network minha-rede ubuntu
```

Então, a partir do terminal de `meu-segundo-container` podemos dar `ping meu-container`

> Obs: para usar o ping, tem que instalar utilizando `apt-get install iputils-ping`

Podemos ver quais containers estão na rede com o comando

```
docker network inspect minha-rede
```

> OBS: Subir primeiro o banco de dados e depois o site

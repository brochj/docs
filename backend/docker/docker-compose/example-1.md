# Docker Compose
## Exemplo 4 containers

Vamos fazer uma aplicação que tem um `nginx` (load balancer), que é quem vai receber as requesições e vai distribuir de forma balanceada para três containers `nodejs`, e esses três `nodejs` vão ter acesso a um banco `mongo`

```sh
        |── Nodejs 1 ───| 
Nginx ──|── Nodejs 2 ───|── MongoDB
        |── Nodejs 3 ───| 

```

1. Criar uma pasta "docker"

```sh
├── docker
│   ├── alura-books.dockerfile
│   ├── config
│   │   └── nginx.conf
│   └── nginx.dockerfile

```
### alura-books.dockerfile

```dockerfile
FROM node:latest
MAINTAINER Douglas Quintanilha
ENV NODE_ENV=development
COPY . /var/www
WORKDIR /var/www
RUN npm install 
ENTRYPOINT ["npm", "start"]
EXPOSE 3000

```

### nginx.dockerfile

```dockerfile
FROM nginx:latest
MAINTAINER Douglas Quintanilha
COPY /public /var/www/public
COPY /docker/config/nginx.conf /etc/nginx/nginx.conf
RUN chmod 755 -R /var/www/public
EXPOSE 80 443
ENTRYPOINT ["nginx"]
# Parametros extras para o entrypoint
CMD ["-g", "daemon off;"]
```

2. Criar no root do projeto o arquivo `docker-compose.yml`

```yaml
version: '3' # versão do compose
services:  # cada service é um container
    nginx: 
        build: 
            dockerfile: ./docker/nginx.dockerfile
            context: .
        image: brock/nginx # nome vou dar para a  imagem que vou buildar
        container_name: nginx
        ports:
            - "80:80"
        networks: 
            - production-network
        depends_on:
            - "node1"
            - "node2"
            - "node3"

    mongodb:
        image: mongo # vou usar uma imagem padrão, não precisa buildar
        networks: 
            - production-network

    node1:
        build:
            dockerfile: ./docker/alura-books.dockerfile
            context: .  # caminho que vou utilizar durante o build
        image: brock/alura-books
        container_name: alura-books-1
        ports:
            - "3000"
        networks:
            - production-network
        depends_on: # definindo a ordem que será criado os containers
            - "mongodb" # node1 só start depois que mongodb estiver startado  

    node2:
        build:
            dockerfile: ./docker/alura-books.dockerfile
            context: .  # caminho que vou utilizar durante o build
        image: brock/alura-books
        container_name: alura-books-2
        ports:
            - "3000"
        networks:
            - production-network
        depends_on: # definindo a ordem que será criado os containers
            - "mongodb" #   node2 só start depois que mongodb estiver startado

    node3:
        build:
            dockerfile: ./docker/alura-books.dockerfile
            context: .  # caminho que vou utilizar durante o build
        image: brock/alura-books
        container_name: alura-books-3
        ports:
            - "3000"
        networks:
            - production-network
        depends_on: # definindo a ordem que será criado os containers
            - "mongodb" # node3 só start depois que mongodb estiver startado  

networks:
    production-network: # nome da minha network
        driver: bridge

```
3. Comandos para subir os containers

Na pasta onde esta o `docker-compose.ym` rodar o seguinte comando para buildar as imagens que são necessárias buildar

```
docker-compose build
```

Depois para subir os containers

```
docker-compose up
```

Também podemos usar o `-d` para liberar o terminal

```
docker-compose up -d

```

Para ver os containers

`docker ps` ou `docker-compose ps`

Para fechar os containers

```
docker-compose down

```
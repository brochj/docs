# Run Nodejs using Docker

First create a `.dockerignore` file in the same directory as your `.dockerfile` with following content:

```sh
node_modules
npm-debug.log
```

## Example 1

Create a Dockerfile

```dockerfile
FROM node:alpine
WORKDIR /user/app
COPY package.json ./
RUN npm install
COPY . .
EXPOSE 3333
CMD ["npm","run","dev"]
```

Build the image

```sh
docker build -t <image-name>
```

Run the image

```sh
docker run -d -p 3333:3333 <image-name>
```

start the container

```sh
docker start <container-id>
```

## Example 2

Create a Dockerfile

```dockerfile
FROM node:16
# Create app directory
WORKDIR /usr/app
COPY package*.json ./
RUN npm install -g npm@8.1.3
RUN npm install
# If you are building your code for production
# RUN npm ci --only=production
COPY . .
EXPOSE 3333
ENTRYPOINT [ "npm", "run", "dev" ]
```

Build the image

```sh
docker build -f <arquivo-dockerfile> -t <nome-da-imagem> <pasta-onde-esta-projeto>

# example
docker build -f nodeapi.dockerfile -t brock/nodeapi .
```

Run the container

```sh
docker run --name mynodejsapi -d -p <host-port>:<container-port> <image-name>
# example
docker run --name mynodejsapi -d -p 3333:3333 brock/nodeapi
```

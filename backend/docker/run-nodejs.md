## Run Nodejs using Docker

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
docker start <imaga-id>
```
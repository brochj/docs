# Docker

## Instalando o Docker
- Pesquisar por [**docker ce**](https://docs.docker.com/install/linux/docker-ce/ubuntu/) e seguir os passos de instalação.

- Depois de instalado realizar o [postinstall](https://docs.docker.com/install/linux/linux-postinstall/) para evitar usar `sudo` toda hora que for utilizar o comando `docker`. (requer um reboot da máquina para aplicar as mudanças).
  
- No Postinstall não configurar para start on boot.

- Rodar `docker -v` e `docker run hello-world` para ver se está tudo certo. 

## Criando o Database
- Pesquisar por [docker postgres](https://hub.docker.com/_/postgres) lá terá como utilizar a imagem

> $docker run --name some-postgres -e POSTGRES_PASSWORD=mysecretpassword -d postgres

- Exemplo
```bash
  docker run --name meetappDB -e POSTGRES_PASSWORD=docker -p 5432:5432 -d postgres
```
- Redirecionamento de portas `-p`
```bash
-p portaDoPC:portaDoContainer
```
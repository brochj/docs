# Deploy de app em NodeJs

## Acesso à máquina

> Exemplo utilizando a Digital Ocean, distro ubuntu com docker.

- Com o IP do máquina, dar o comando

```bash
ssh root@IP.Da.Maq.aqui
```

```bash
#Exemplo
ssh root@165.22.35.148
```

## Atualizar a máquina

```bash
apt update
```

```bash
apt upgrade
```

## Criando usuário

- Interessante criar um novo usuário, para não ficar manipulando dentro do usuário **root**

```bash
adduser deploy
```

- Colocar um senha
- O resto, `full name`, `room number`, etc, não é necessário preencher.
- Dar permissões de adm para este usuário, para que ele consiga executar comandos com `sudo`.

```bash
usermod -aG sudo <UserName>
```

```bash
# Exemplo
usermod -aG sudo deploy
```

## Habilitando conexão SSH

- Para permitir que as conexões SSH sejam feitas também direto pelo novo usuário criado.

- Criar pasta `.ssh`

```bash
cd /home/deploy && mkdir .ssh
```

- Copiar os arquivos do usuário root para o usuário criado.

```bash
cp ~/.ssh/authorized_keys /home/deploy/.ssh
```

- Dar um `ls -la` dentro da pasta `/home/deploy/.ssh` para ver se o arquivo `authorized_keys` está lá dentro.

```bash
# output
-rw------- 1 root root 423 jul 22 16:45 authorized_keys
```

- Alterar o dono do arquivo (`root root`) para o user deploy

```bash
chown deploy:deploy authorized_keys
```

### Testando

- Dar o comando `exit` para sair da máquina e voltar para sua máquina
- Refazer a conexão, trocando o `root` por `deploy` com o comando

```bash
ssh deploy@165.22.35.148
```

- A conexão deve ser feita. E agora caso precise instalar dependências que precisam de permissão root é só dar `sudo` e passar a senha que foi definida na criação do usuário.

## Configurando a máquina

### Git

- Verificar se tem o Git, se não , instale

### Nodejs

- Instalar a **versão LTS** via package manager.

  > Debian and Ubuntu based Linux distributions, Enterprise Linux/Fedora and Snap packages
  >
  > #### [Official Node.js binary distributions are provided by NodeSource](https://github.com/nodesource/distributions/blob/master/README.md)

- NodeJS 10.x LTS (no momento da criação deste post)

```bash
curl -sL https://rpm.nodesource.com/setup_10.x | bash -
```

```bash
sudo apt-get install -y nodejs
```

- Verificando

```bash
node -v
```

```bash
npm -v
```

# Copiando a aplicação

- Neste caso utilizaremos o Git e Github.
- Criar um repositório no Github com a aplicação nele

- Na pasta `cd ~` dar o git clone.

> Se o repositorio for privado, será necessário adicionar o login e senha nas config do Git

```bash
~$ git clone https:// .....
```

- Entrar na pasta do projeto e dar o comando `npm install` para ele baixar as dependências do projeto.

## Configurar o Dotenv

- Na pasta do projeto

```bash
cp .env.example .env
```

- Abrir o arquivo `.env` com o vim ou nano

```bash
vim .env
```

- Trocar para

```bash
APP_URL=http://165.22.35.148:3333

NODE_ENV=production

APP_SECRET=criar_um_secret_bem_complexo_apenas_para_quanto_estiver_em_producao

DB_HOST=localhost
DB_USER=postgres
DB_PASS=suasenhasuperforte
DB_NAME=nomedadatabasepostgres

MONGO_URL=mongo://localhost:27017/nomedadatabase

REDIS_HOST=127.0.0.1
REDIS_POST=6379

```

## Configurar Docker

- Como na criação do servidor foi escolhido um que vem com Docker instalado, única coisa necessária é realizar o [**post Install**](https://docs.docker.com/install/linux/linux-postinstall/) do docker para que seja possível executar comandos sem precisar do `sudo`.
- Esse post install é basicamente:

```bash
sudo groupadd docker
```

```bash
sudo usermod -aG docker $USER
```

- Depois deslogar da conexão utilizando o `exit` e conectar denovo

- Verificando se funcionou é só tentar rodar um `docker ps` sem utilizar o `sudo`.

## Configurar os Databases

### Postgres

```bash
docker run --name postgres -e POSTGRES_PASSWORD=suasenhasuperforte -p 5432:5432 -d -t postgres
```

- Criando a base de dados

```bash
docker exec -i -t postgres /bin/sh
```

- Após rodar esse comando, você estará dentro do terminal do conteiner do postgres (que também é uma distro linux)
- Mudar de usuário com `su postgres` e rodar o comando `psql`

- O `psql` é a interface de linha de comando do postgres

- **OBS:** `nomedadatabasepostgres` tem que ser o mesmo que foi definido no **`.env`**

- Dentro `psql` dar o comando:

```bash
CREATE DATABASE nomedadatabasepostgres;
```

- Dar um `\q` para sair do `psql`, depois dois comandos `exit` em seguida para voltar até o usuário **deploy**

- Rodar as migrations:

```bash
npx sequelize db:migrate
```

### Mongo

```bash
docker run --name mongo -p 27017:27017 -d -t mongo
```

### Redis

```bash
docker run --name redis -p 6379:6379 -d -t redis:alpine
```

- Rodar `docker ps` para ver se os três containeres estão rodando.

## Rodando o server

- Passos Gerais
  - Vamos fazer algumas alterações no projeto (Não no projeto do servidor).
  - Subir para Github
  - E depois faremos o `pull` do projeto, aí sim dentro do servidor.

### No package.json

- Fazer as seguintes alterações nos `scripts`
- Vamos adicionar dois novos scripts
- `build` : Vai gerar o bundle que ficará na pasta `./dist`
- `start` : Vai rodar a aplicação utilizando o bundle criado.

```json
{
  "scripts": {
    (...)
    "build": "sucrase ./src -d ./dist --transforms imports",
    "start": "node dist/server.js"
  }
}
```

- Testar os comandos `yarn build` e `yarn start`
- Se o `yarn start` falhar pode ser que os bancos de dados não estejam rodando.

### No .gitignore

- A pasta `./dist` não deve ir para o github, então adicionar a linha `dist/` no arquivo.

- Depois de fazer as alterações, fazer o `commit` e `push`.

### No servidor

- Dar o comando `git pull`
- Abrir o arquivo `package.json` e verificar se os scripts de `build` e `start` estão lá.
- Verificar se os databases e serviços estão rodando.
- Verificar se foi feito as migrations, se não, na pasta da aplicação rodar:

```bash
npx sequelize db:migrate
```

- Rodar a aplicação com

```bash
npm run build
```

e depois

```bash
npm run start
```

## Verificando

- No insomnia trocar a `base_url` para o Ip do server
- exemplo: `http://http://165.22.35.148:3333`
- Tentar fazer uma request

- Em caso de erro, provavelmente a porta do servidor está bloqueada por firewall, para liberar o acesso externo nessa porta, rodar o comando.

```bash
sudo ufw allow 3333
```

- A aplicação já deve estar funcionando, porém ainda é necessário mais algumas alterações, para que se possa acessar sem tem que passa a `porta 3333`

## Dicas SSH

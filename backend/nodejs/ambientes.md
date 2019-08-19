
# Configurando ambiente Nodejs

<!-- Rckt -->

### Instalando nvm

1. Instalar o `nvm` para controlar as versões do nodejs
2. Instalar a(s) versão(ões) do nodejs desejada(s)  
```bash
nvm install 10.15.3
```
3. Escolher a versão default
```bash
nvm alias default 10.15.3
```
4. Verificar a instalção
```bash
node -v && npm -v
```
---
### Conceitos de Node.js
#### O que é Node.js?

1. Plataforma para desenvolver o backend(não é uma linguagem)
2. Construído em cima da V8, que é a máquina que roda por trás do chrome

3. Javascript no backend
  - Não lidamos com eventos do usuário final

4. Rotas e integrações
  - Quando o usuário acessa alguma rota, podemos disparar algum código do Node para ser executado 

#### Características
- Arquitetura Event-Loop
  - Baseada em eventos (rotas na maioria das vezes)
  - Call Stack (last in, first out)
  - A função que vier mais tarde na pilha(stack) será a primeira a ser processada
- Node single-thread
  - C++ por trás com libuv
  - Background threads
- Non-blocking I/O
  - Pode enviar os dados para o cliente/servidor em partes. O que possibilita conexões em tempo real

#### Frameworks
- O framework mais famoso de node é o **ExpressJS**
  - Não possui estrutura fechada
  - Possui apenas o essencial
  - Micro-serviços

- **AdonisJS**
- **NestJS**

---
### Conceitos de API REST

#### Como funciona uma API
1. Uma requisição é feita por cliente
2. O backend retorna através de uma estrutura de dados
3. Cliente recebe a reposta e processa o resultado. Ou seja o frontend fica responsável por montar a interface de acordo com os dados recebidos.
4. As rotas utilizam os métodos HTTP
  - GET
  - POST
  - PUT
  - DELETE
  
Exemplo:
```http
PUT - http://api.com/user/1
```
O `user` é denomidado comom recurso/rota. O `1` é um parâmetro que enviado dentro do URL

#### Vantagens de uma API Rest
- **Multiplataforma**, ou seja, o frontend pode ser web, mobile, desktop, api pública. Pois é o frontend que fica encarregado de mostrar as informações para o usuário.
- Protocolo da comunicação padronizado (mais utilizado JSON)

#### Conteúdo da requisição

##### Utilizando GET
```http
GET http://api.com/company/1/users?page=2
```
- Routes = `company`,`users`
- Routes params = `1`
- Query params = `?page=2`

##### Utilizando o POST
```js
POST http://api.com/company/1/users
```
- **Body**
```json
{
  "user": "Oscar Broch",
  "email": "brochj@gmail.com"
}
```
  - Utiliza-se o Body para enviar os parâmetros(request body)
  - Utilizado somente em POST e PUT
  - Usando `request body` os dados do usuário não aparacem na URL do navegador  

- **Headers**
```json
{
  "locale": "pt_BR"
}
```
- São infos adicionais que não tem a ver com a o requisição do usuário.
- Utilizado para autenticacão, locale, etc.
 ---- 
### HTTP codes
Toda resposta que o backend retorna possui um `HTTP code`, código de três dígitos numéricos que demostram o status daquela resposta.

- `1xx`:Informational
- `2xx`: Success
  - 200: Success
  - 201: Created
- `3xx`: Redirection
  - 301: moved permanently
  - 302: moved
- `4xx`: Client Error
  - 400: bad request
  - 401: unauthorized
  - 404: not found 
- `5xx`: Server Error
  - 500: Internal server error
****
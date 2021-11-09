# Enviar email

## Configurando o Nodemailer

- instalar o nodemailer

```bash
yarn add nodemailer
```

- criar um `config/mail.js`

```js
export default {
  host: "",
  port: "",
  secure: false,
  auth: {
    user: "",
    pass: "",
  },
  default: {
    from: "Equipe MeetApp <noreply@meetapp.com>",
  },
};
```

- Procurar por um servico de envio de email. exemplos:

  - Amazon SES,
  - Mailgun
  - Sparkpost
  - Mandril (soh pode ser utilizado por quem usa o mailchimp)
  - Gmail (nao utilizar o pq tem um limite baixo)
  - Mailtrap (soh funciona em ambiente de desenvolvimento)

- Criar pasta `src/lib/Mail.js`. Essa pasta lib vai guardar todos os sevicos externos a aplicacao

```js
import nodemailer from "nodemailer";
import mailConfig from "../config/mail";

class Mail {
  constructor() {
    const { host, port, secure, auth } = mailConfig;

    this.transporter = nodemailer.createTransport({
      host,
      port,
      secure,
      auth: auth.user ? auth : null,
    });
  }

  sendMail(message) {
    return this.transporter.sendMail({
      ...mailConfig.default,
      ...message,
    });
  }
}

export default new Mail();
```

- Para testar, adicionar o codigo dentro de algum controller

```js
import Mail from '../../lib/Mail';
...
await Mail.sendMail({
      to: `${meetup.user.name} <${meetup.user.email}>`,
      subject: 'Nova inscrição',
      text: 'Houve uma nova inscrição',
    });
```

- depois de fazer a requisição deve aparecer o email na caixa de entrada no MailTrap. Obs: essa requiscao vai demorar mais, algo entre 2~3 seg. Para deixar mais rápido deve-se impementar um sistema de Queue.

# Templates de email

## Configurando

- Necessário instalar duas libs para poder utilizar o template engine no node.
- template engine são basicamente arquivos html que podem receber variáveis do node. (tem muito mais funcionalidade)
- O template engine utilizado será o `handlebars` (tem muitos outros)
- Instalar

```bash
yarn add express-handlebars nodemailer-express-handlebars
```

## Criar os arquivos

- dentro da pasta `app` criar a seguinte estrutura.
- `subscription.hbs` é o template a ser criado. Podem criar outros.

```bash
app
└──views
    └── emails
        ├── layouts
        │   └── default.hbs
        ├── partials
        └── subscription.hbs
```

## Configurando Mail.js

- Em `src/lib/Mail.js`

- importar as duas lib instaladas

```js
import nodemailer from "nodemailer";
import { resolve } from "path";
import exphbs from "express-handlebars";
import nodemailerhbs from "nodemailer-express-handlebars";
import mailConfig from "../config/mail";

class Mail {
  constructor() {
    const { host, port, secure, auth } = mailConfig;

    this.transporter = nodemailer.createTransport({
      host,
      port,
      secure,
      auth: auth.user ? auth : null,
    });

    this.configureTemplates();
  }

  configureTemplates() {
    const viewPath = resolve(__dirname, "..", "app", "views", "emails");

    this.transporter.use(
      "compile",
      nodemailerhbs({
        viewEngine: exphbs.create({
          layoutsDir: resolve(viewPath, "layouts"),
          partialsDir: resolve(viewPath, "partials"),
          defaultLayout: "default",
          extname: ".hbs",
        }),
        viewPath,
        extName: ".hbs",
      })
    );
  }

  sendMail(message) {
    return this.transporter.sendMail({
      ...mailConfig.default,
      ...message,
    });
  }
}

export default new Mail();
```

## Criando partials

- Partials são como components, são arquivos que podem ser importados para dentro de layouts ou templates. Exemplo um footer, header, etc. Algo que se repete em diferentes tipos de emails.
- criar em `partials/footer.hbs`

```html
<br />
Equipe MeetApp
```

## Configurando o Layout

- `layouts/default.hbs` é o layout que será utilizado em todos os envios de email.
- Dentro do arquivo `default.hbs`

```html
<div
  style="font-family: Arial, Helvetica, sans-serif;
font-size:16px;
line-height: 1.6;
color: #222;
max-width: 600px;
"
>
  {{{ body }}} {{> footer}}
</div>
```

- O {{{body}}} vai ser substituido pelo `subscription.hbs`

## Criando o template

- dentro do `emails/subscription.hbs`

```html
<strong> Olá, {{ meetupCreator }}</strong>

<p>Houve uma nova inscrição em seu Meetup, confira os detalhes abaixo:</p>

<p>
  <strong>Meetup: </strong> {{ meetup_title }} <br />
  <strong>Nome: </strong> {{ user }} <br />
</p>
```

## Usando os templates

- Voltar no controller e alterar o método `sendMail()`

```js
await Mail.sendMail({
  to: `${meetup.user.name} <${meetup.user.email}>`,
  subject: `Nova inscrição em ${meetup.title}`,
  template: "subscription",
  context: {
    meetupCreator: meetup.user.name,
    meetup_title: meetup.title,
    user: user.name,
  },
});
```

- `context` : Tem receber todas as variáveis que foram utilizadas dentro do template `subscription.hbs`

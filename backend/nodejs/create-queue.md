# Criando Queue's

- A melhor forma de controlar acoes que levam um tempo maior e elas nao precisam finalizar no mesmo momento que é retornada a resposta para o usuario, mas mesmo assim a gente quer ter controle dessas acoes, para ver se elas deram erros, fazer retentativas, dar prioridade para que algumas acoes ocorram antes de outras. A melhor forma de fazer isso é utilizando *Queue's* (filas, *background jobs*)

No caso de envio de email é interessante criar uma queue para que, além do ganho de tempo de reposta na requisição, tenha-se controle desse envio, em poucas palavras, será possível saber se houve algum erro durante esse envio.

## Configurando os background Job
- Precisa-se de um banco chave-valor
- Utilizar o `Redis`. É um banco não relacional, porém ele não possui schemas, estrutura de dados. Só possivel salvar chave e valor.
- Por não ter estrutura ele é ainda mais perfomático que o mongoDB, pode ter milhares e milhares de registros que ele ainda continua sendo perfomático.

### Instalando o Redis
```bash
docker run --name redismeetapp -p 6379:6379 -d -t redis:alpine
```

## Instalando o bee-queue
- O `bee-queue` é uma ferramente de fila dentro do node de background jobs extremamente performático 
- Com ele não é possível trabalhar com prioridades (para isso utilizar o `kue`)
- No caso de enviar emails o bee-queue serve, pois com ele é possivel fazer retentativas

```bash
yarn add bee-queue
```


### Criando um job
- criar um arquivo em `scr/app/jobs/SubscriptionMail.js`

```js
import { format,parseISO } from 'date-fns';
import pt from 'date-fns/locale/pt';
import Mail from '../../lib/Mail';

class SubscriptionMail {
  get key() {
    return 'SubscriptionMail'; // return a unique key
  }

  // handle é tarefa a ser executada para cada email na fila
  async handle({ data }) {
    const { user, meetup } = data;

    await Mail.sendMail({
      to: `${meetup.User.name} <${meetup.User.email}>`,
      subject: `Nova inscrição em ${meetup.title}`,
      template: 'subscription',
      context: {
        meetupCreator: meetup.User.name,
        meetup_title: meetup.title,
        user: user.name,
        date: format(
          parseISO(meetup.date), "dd 'de' MMMM' de ' yyyy', às' H:mm'h'", {
          locale: pt,
        }),
      },
    });
  }
}

export default new SubscriptionMail();

```
### Configurando o bee-queue
- Criar em `src/lib/Queue.js`
- Esse arquivo vai funcionar semelhante ao loader de model em `database/index.js`. Só que em vez de carregar os models, esse arquivos irá carregar os ***jobs*** de `scr/app/jobs`.
- Antes, criar a configuração do redis em `config/redis.js`
```js
export default {
  host: '127.0.0.1',
  port: 6379,
};
```

```js
//  src/lib/Queue.js
import Bee from 'bee-queue';
import SubscriptionMail from '../app/jobs/SubscriptionMail';
import redisConfig from '../config/redis';

const jobs = [SubscriptionMail];

class Queue {
  constructor() {
    this.queues = {};

    this.init();
  }

  init() {
    jobs.forEach(({ key, handle }) => {
      this.queues[key] = {
        bee: new Bee(key, {
          redis: redisConfig,
        }),
        handle,
      };
    });
  }
  // add job into queues
  add(queue, job){
    return this.queues[queue].bee.createJob(job).save();
  }

  // process the queues
  processQueue() {
    jobs.forEach(job => {
      const { bee, handle } = this.queues[job.key];

      bee.process(handle);
    });
  }
}

export default new Queue();
```
- Cada tipo de email terá que ter sua própria fila
- Exemplo: uma fila de emails para recuperacao de senha, outra fila para avisar por email os cancelamentos de algum servico, etc.
- Ou seja, cria-se um fila para cada *background job* diferente na aplicação.
- Toda vez que tem uma adição de um job (`add()`), o `processQueue()` é executado.

### Adicionando job na fila
- Voltado ao `SubscriptionController.js`
- Importar a o loader de Queue e o Job

```js
...
import SubscriptionMail from '../jobs/SubscriptionMail';
import Queue from '../../lib/Queue';
...
...
 await Queue.add(SubscriptionMail.key, { meetup, user });
```

### Executando a fila em paralelo
- Criar um arquivo em `src/queue.js`

```js
import Queue from './lib/Queue';

Queue.processQueue();
```
- Adicionar um comando no script do `package.json`

```json
"scripts": {
    "dev": "nodemon src/server.js",
    "queue": "nodemon src/queue.js"
  },
```
- Para executar, abrir um novo terminal na raiz do projeto e

```bash
yarn queue
```
- Para verificar se funcionou, adicionar o `console.log('A fila executou');` dentro do método handle e fazer a requisição e verificar se apareceu a mensagem terminal da queue e o email no Mailtrap.
- Depois de adicionar esse sistema de Queues, o retorno da requição não deve mais demorar 2~3seg como antes. deve voltar a fincar na casa dos 50~200ms.

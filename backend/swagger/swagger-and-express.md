# SwaggerUI and Express.js

Better Documentation at
[Github: swagger-ui-express](https://github.com/scottie1984/swagger-ui-express)

### Add to project
```sh
npm install swagger-ui-express
```

## Using JSON

### Create the file `swagger.json`
```json
{
    "swagger": "2.0",
    "info": {
      "version": "1.0.0", 
      "title": "Diet App",
      "description": "Diet App API",
      "license": {
        "name": "MIT",
        "url": "https://opensource.org/licenses/MIT"
      }
    },
    "host": "localhost:3000",
    "basePath": "/",
    "tags": [
      {
        "name": "Users",
        "description": "API for users in the system"
      }
    ],
    "schemes": ["http"],
    "consumes": ["application/json"],
    "produces": ["application/json"]
  }
```

### Add a new route

```js
import swaggerUi from 'swagger-ui-express';
import swaggerDocument from '../swagger.json';

routes.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
```
### Start the API

Now Open the browser with http://localhost:3333/api-docs/
and you will able to see the swagger UI for documentation.

---

## Using Javascript Object

### Create the file `swagger.js`
```js
export const swaggerDocument = {
  openapi: '3.0.1',
  info: {
    version: '1.0.0',
    title: 'APIs Document',
    description: 'your description here',
    termsOfService: '',
    contact: {
      name: 'Tran Son hoang',
      email: 'son.hoang01@gmail.com',
      url: 'https://hoangtran.co',
    },
    license: {
      name: 'Apache 2.0',
      url: 'https://www.apache.org/licenses/LICENSE-2.0.html',
    },
  },
  host: 'localhost:3000',
  basePath: '/',
  tags: [
    {
      name: 'Users',
      description: 'API for users in the system',
    },
  ],
  schemes: ['http'],
  consumes: ['application/json'],
  produces: ['application/json'],
};

```

### Add a new route

```js
import swaggerUi from 'swagger-ui-express';
import { swaggerDocument } from './swagger.json';

routes.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
```
### Start the API

Now Open the browser with http://localhost:3333/api-docs/

and you will able to see the swagger UI for documentation.
## Using YAML file

### Create the file `swagger.yaml`
```yaml
TODO
```

### Add a new route

```js
const swaggerUi = require('swagger-ui-express');
const YAML = require('yamljs');
const swaggerDocument = YAML.load('./swagger.yaml');

routes.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
```
### Start the API

Now Open the browser with http://localhost:3333/api-docs/
and you will able to see the swagger UI for documentation.

## Two swagger documents

To run 2 swagger ui instances with different swagger documents, use the serveFiles function instead of the serve function. The serveFiles function has the same signature as the setup function.

```js
const express = require('express');
const app = express();
const swaggerUi = require('swagger-ui-express');
const swaggerDocumentOne = require('./swagger-one.json');
const swaggerDocumentTwo = require('./swagger-one.json');

var options = {}

app.use('/api-docs-one', swaggerUi.serveFiles(swaggerDocumentOne, options), swaggerUi.setup(swaggerDocumentOne));

app.use('/api-docs-two', swaggerUi.serveFiles(swaggerDocumentTwo, options), swaggerUi.setup(swaggerDocumentTwo));
```
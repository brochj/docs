# SwaggerUI and Express.js

## Add to project
```sh
npm install swagger-ui-express -S
```

## Create the file `swagger.json`
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

## Add a new route

```js
import swaggerUi from 'swagger-ui-express';
import swaggerDocument from '../swagger.json';

routes.use('/api-docs', swaggerUi.serve, swaggerUi.setup(swaggerDocument));
```
## Start the API

Now Open the browser with http://localhost:3333/api-docs/
and you will able to see the swagger UI for documentation.
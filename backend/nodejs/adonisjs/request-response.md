# Request and Responses

## Request

`http://127.0.0.1:3333/api/painel/?idade=18&nome=joao`

Controller

```js
async index ({ request }){ 
  return {
    response: "index do Painel",
    qs: request.qs(),
    url: request.url(),
    completeUrl: request.completeUrl(),
    all: request.all(),
    only: request.only(['idade']),
    except: request.except(['idade']),
    ip: request.ip(),
    ips: request.ips(),
    language: request.language(),
    method: request.method(),
    headers: request.headers(),
    request

  }
}
```

Resposta

```json
{
  "response": "index do Painel",
  "qs": {
    "idade": "18",
    "nome": "joao"
  },
  "url": "/api/painel/",
  "completeUrl": "http://127.0.0.1:3333/api/painel/",
  "all": {
    "idade": "18",
    "nome": "joao"
  },
  "only": {
    "idade": "18"
  },
  "except": {
    "nome": "joao"
  },
  "ip": "127.0.0.1",
  "ips": [
    "127.0.0.1"
  ],
  "language": [
    "en-US",
    "en",
    "pt",
    "la"
  ],
  "method": "GET",
  "headers": {
    "host": "127.0.0.1:3333",
    "connection": "keep-alive",
    "cache-control": "max-age=0",
    "sec-ch-ua": "\" Not A;Brand\";v=\"99\", \"Chromium\";v=\"96\", \"Google Chrome\";v=\"96\"",
    "sec-ch-ua-mobile": "?0",
    "sec-ch-ua-platform": "\"Linux\"",
    "upgrade-insecure-requests": "1",
    "user-agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36",
    "accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
    "sec-fetch-site": "none",
    "sec-fetch-mode": "navigate",
    "sec-fetch-user": "?1",
    "sec-fetch-dest": "document",
    "accept-encoding": "gzip, deflate, br",
    "accept-language": "en-US,en;q=0.9,pt;q=0.8,la;q=0.7",
    "cookie": "adonis-session=s%3AeyJtZXNzYWdlIjoiY2t4Z2NxNTVpMDAwMGl0bXloM2JhZ3ZqdCIsInB1cnBvc2UiOiJhZG9uaXMtc2Vzc2lvbiJ9.BNkShQhe7Uc6fG4kW62ZR6yTCSDEFOB1I_2lSkUyzOk; ckxgcq55i0000itmyh3bagvjt=e%3AuZDmT6yCpd5Wcgox9OpGhxINrCw6NfIexSwVffvyP5_2JhKrDs45ZeZRNw0sjZJ9DwjPEYgBYuhWwMzfvw84LA.SEV2d21VU3NQalNUVjI5Uw.lyqxlcVahEPc4h5aYIBDRxCk8b4Oun-SefA8IbSV6kM"
  },
  "request": {
    "url": "/api/painel/",
    "query": "idade=18&nome=joao",
    "body": {
      "idade": "18",
      "nome": "joao"
    },
    "params": {
      
    },
    "headers": {
      "host": "127.0.0.1:3333",
      "connection": "keep-alive",
      "cache-control": "max-age=0",
      "sec-ch-ua": "\" Not A;Brand\";v=\"99\", \"Chromium\";v=\"96\", \"Google Chrome\";v=\"96\"",
      "sec-ch-ua-mobile": "?0",
      "sec-ch-ua-platform": "\"Linux\"",
      "upgrade-insecure-requests": "1",
      "user-agent": "Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.110 Safari/537.36",
      "accept": "text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9",
      "sec-fetch-site": "none",
      "sec-fetch-mode": "navigate",
      "sec-fetch-user": "?1",
      "sec-fetch-dest": "document",
      "accept-encoding": "gzip, deflate, br",
      "accept-language": "en-US,en;q=0.9,pt;q=0.8,la;q=0.7",
      "cookie": "adonis-session=s%3AeyJtZXNzYWdlIjoiY2t4Z2NxNTVpMDAwMGl0bXloM2JhZ3ZqdCIsInB1cnBvc2UiOiJhZG9uaXMtc2Vzc2lvbiJ9.BNkShQhe7Uc6fG4kW62ZR6yTCSDEFOB1I_2lSkUyzOk; ckxgcq55i0000itmyh3bagvjt=e%3AuZDmT6yCpd5Wcgox9OpGhxINrCw6NfIexSwVffvyP5_2JhKrDs45ZeZRNw0sjZJ9DwjPEYgBYuhWwMzfvw84LA.SEV2d21VU3NQalNUVjI5Uw.lyqxlcVahEPc4h5aYIBDRxCk8b4Oun-SefA8IbSV6kM"
    },
    "method": "GET",
    "protocol": "http",
    "cookies": {
      "adonis-session": "s:eyJtZXNzYWdlIjoiY2t4Z2NxNTVpMDAwMGl0bXloM2JhZ3ZqdCIsInB1cnBvc2UiOiJhZG9uaXMtc2Vzc2lvbiJ9.BNkShQhe7Uc6fG4kW62ZR6yTCSDEFOB1I_2lSkUyzOk",
      "ckxgcq55i0000itmyh3bagvjt": "e:uZDmT6yCpd5Wcgox9OpGhxINrCw6NfIexSwVffvyP5_2JhKrDs45ZeZRNw0sjZJ9DwjPEYgBYuhWwMzfvw84LA.SEV2d21VU3NQalNUVjI5Uw.lyqxlcVahEPc4h5aYIBDRxCk8b4Oun-SefA8IbSV6kM"
    },
    "hostname": "127.0.0.1",
    "ip": "127.0.0.1",
    "subdomains": {
      
    }
  }
}
```

## Response

o quando retornamos dentro do método, o adonis faz um `response.send()` por baixo dos panos

```js
async index ({ request, response }){ 
  return {
    msg: "index do Painel",
  }
}
```

```js
async index ({ request, response }){ 
  response.send({
    msg: "index do Painel",
  })
}
```

### Passando Status da requisição

```js
async index ({ response }){ 
  response.status(404).send({
    msg: "Not Found",
  })
}
```

### Redirecionando URL

```js
async index ({ response }){ 
  response.redirect().toPath('/api/painel/usuarios/1')
}
```
```js
async index ({ response }){ 
  response.redirect('http://...')
}
```

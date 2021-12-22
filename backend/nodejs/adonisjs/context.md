# Context no AdonisJs

No `objeto context` contém tudo que podemos usar dentro daquele context, seja ele Http, socket..etc.

como contém muitas coisas, destruturamos e pegamos só que precisamos

```js
// import { HttpContextContract } from '@ioc:Adonis/Core/HttpContext'

export default class HomeController {
  async index({ view }) {
    return view.render("painel.homepage");
  }
}
```

Por padrão o Adonis usa o `HttpContextContract`

```js
import { HttpContextContract } from "@ioc:Adonis/Core/HttpContext";

export default class HomeController {
  async index(ctx: HttpContextContract) {
    console.log(ctx);
    return ctx.view.render("painel.homepage");
  }
}
```

Veja o que tem dentro de `HttpContextContract`

```ts
<ref *1> HttpContext {
  request: Request {
    request: IncomingMessage {
      _readableState: [ReadableState],
      _events: [Object: null prototype],
      _eventsCount: 1,
      _maxListeners: undefined,
      socket: [Socket],
      httpVersionMajor: 1,
      httpVersionMinor: 1,
      httpVersion: '1.1',
      complete: true,
      rawHeaders: [Array],
      rawTrailers: [],
      aborted: false,
      upgrade: false,
      url: '/',
      method: 'GET',
      statusCode: null,
      statusMessage: null,
      client: [Socket],
      _consuming: false,
      _dumped: false,
      _parsedUrl: [Url],
      [Symbol(kCapture)]: false,
      [Symbol(kHeaders)]: [Object],
      [Symbol(kHeadersCount)]: 32,
      [Symbol(kTrailers)]: null,
      [Symbol(kTrailersCount)]: 0,
      [Symbol(RequestTimeout)]: undefined
    },
    response: ServerResponse {
      _events: [Object: null prototype],
      _eventsCount: 1,
      _maxListeners: undefined,
      outputData: [],
      outputSize: 0,
      writable: true,
      destroyed: false,
      _last: false,
      chunkedEncoding: false,
      shouldKeepAlive: true,
      _defaultKeepAlive: true,
      useChunkedEncodingByDefault: true,
      sendDate: true,
      _removedConnection: false,
      _removedContLen: false,
      _removedTE: false,
      _contentLength: null,
      _hasBody: true,
      _trailer: '',
      finished: false,
      _headerSent: false,
      _closed: false,
      socket: [Socket],
      _header: null,
      _keepAliveTimeout: 5000,
      _onPendingData: [Function: bound updateOutgoingData],
      req: [IncomingMessage],
      _sent100: false,
      _expect_continue: false,
      parent: [Response],
      [Symbol(kCapture)]: false,
      [Symbol(kNeedDrain)]: false,
      [Symbol(corked)]: 0,
      [Symbol(kOutHeaders)]: null
    },
    encryption: Encryption {
      options: [Object],
      separator: '.',
      base64: Base64 {},
      algorithm: 'aes-256-cbc',
      cryptoKey: <Buffer bc 30 df 58 48 03 4f c0 95 ed d6 e6 4a 99 00 8d 77 7b 49 79 01 58 73 48 53 20 b1 f0 86 bf b2 01>,
      verifier: [MessageVerifier]
    },
    config: {
      allowMethodSpoofing: false,
      subdomainOffset: 2,
      generateRequestId: false,
      trustProxy: [Function: trust],
      etag: false,
      jsonpCallbackName: 'callback',
      cookie: [Object]
    },
    requestBody: {},
    routeParams: {},
    requestData: {},
    originalRequestData: {},
    requestQs: {},
    rawRequestBody: null,
    lazyAccepts: null,
    parsedUrl: Url {
      protocol: null,
      slashes: null,
      auth: null,
      host: null,
      port: null,
      hostname: null,
      hash: null,
      search: null,
      query: null,
      pathname: '/',
      path: '/',
      href: '/'
    },
    ctx: [Circular *1],
    cookieParser: CookieParser {
      cookieHeader: 'adonis-session=s%3AeyJtZXNzYWdlIjoiY2t4aGhraDhjMDAwMHJlbXlmMHNyM3Y0MSIsInB1cnBvc2UiOiJhZG9uaXMtc2Vzc2lvbiJ9.xEFgf2-zVXI-VvkowvV0OWR0-qh_zGRzKHBe_bwN2t4; ckxhhkh8c0000remyf0sr3v41=e%3Ac6wWwRR7xNTH2_TwAryaGNxfpmREsknvlO2GzsOZwyh3tEAmy5rsvlKRKzpQt37icKy3MQepebZjdjAUh7eB2w.NHJMNTRDU1hfTW5ySlM2NA.58qUDappDNad_Nn-sElVnTpMy-EoaU-4_laKDakYdUM',
      encryption: [Encryption],
      client: [CookieClient],
      cachedCookies: [Object],
      cookies: [Object]
    },
    __raw_files: {}
  },
  response: <ref *2> Response {
    request: IncomingMessage {
      _readableState: [ReadableState],
      _events: [Object: null prototype],
      _eventsCount: 1,
      _maxListeners: undefined,
      socket: [Socket],
      httpVersionMajor: 1,
      httpVersionMinor: 1,
      httpVersion: '1.1',
      complete: true,
      rawHeaders: [Array],
      rawTrailers: [],
      aborted: false,
      upgrade: false,
      url: '/',
      method: 'GET',
      statusCode: null,
      statusMessage: null,
      client: [Socket],
      _consuming: false,
      _dumped: false,
      _parsedUrl: [Url],
      [Symbol(kCapture)]: false,
      [Symbol(kHeaders)]: [Object],
      [Symbol(kHeadersCount)]: 32,
      [Symbol(kTrailers)]: null,
      [Symbol(kTrailersCount)]: 0,
      [Symbol(RequestTimeout)]: undefined
    },
    response: ServerResponse {
      _events: [Object: null prototype],
      _eventsCount: 1,
      _maxListeners: undefined,
      outputData: [],
      outputSize: 0,
      writable: true,
      destroyed: false,
      _last: false,
      chunkedEncoding: false,
      shouldKeepAlive: true,
      _defaultKeepAlive: true,
      useChunkedEncodingByDefault: true,
      sendDate: true,
      _removedConnection: false,
      _removedContLen: false,
      _removedTE: false,
      _contentLength: null,
      _hasBody: true,
      _trailer: '',
      finished: false,
      _headerSent: false,
      _closed: false,
      socket: [Socket],
      _header: null,
      _keepAliveTimeout: 5000,
      _onPendingData: [Function: bound updateOutgoingData],
      req: [IncomingMessage],
      _sent100: false,
      _expect_continue: false,
      parent: [Circular *2],
      [Symbol(kCapture)]: false,
      [Symbol(kNeedDrain)]: false,
      [Symbol(corked)]: 0,
      [Symbol(kOutHeaders)]: null
    },
    encryption: Encryption {
      options: [Object],
      separator: '.',
      base64: Base64 {},
      algorithm: 'aes-256-cbc',
      cryptoKey: <Buffer bc 30 df 58 48 03 4f c0 95 ed d6 e6 4a 99 00 8d 77 7b 49 79 01 58 73 48 53 20 b1 f0 86 bf b2 01>,
      verifier: [MessageVerifier]
    },
    config: {
      allowMethodSpoofing: false,
      subdomainOffset: 2,
      generateRequestId: false,
      trustProxy: [Function: trust],
      etag: false,
      jsonpCallbackName: 'callback',
      cookie: [Object]
    },
    router: Router {
      encryption: [Encryption],
      routeProcessor: [Function (anonymous)],
      routes: [],
      BriskRoute: [Function],
      RouteGroup: [Function],
      RouteResource: [Function],
      Route: [Function],
      RouteMatchers: [Function],
      matchers: RouteMatchers {},
      paramMatchers: {},
      lookupStore: [LookupStore],
      store: [Store],
      openedGroups: []
    },
    headers: {},
    explicitStatus: false,
    writerMethod: 'endResponse',
    cookieSerializer: CookieSerializer {
      encryption: [Encryption],
      client: [CookieClient]
    },
    hasLazyBody: false,
    lazyBody: [],
    ctx: [Circular *1]
  },
  logger: Logger {
    config: {
      name: 'hello-world',
      enabled: true,
      level: 'info',
      prettyPrint: true
    },
    pino: EventEmitter {
      trace: [Function: noop],
      debug: [Function: noop],
      info: [Function: LOG],
      warn: [Function: LOG],
      error: [Function: LOG],
      fatal: [Function (anonymous)],
      [Symbol(pino.serializers)]: [Object: null prototype],
      [Symbol(pino.formatters)]: [Object],
      [Symbol(pino.chindings)]: ',"pid":7807,"hostname":"broch-pc","name":"hello-world"',
      [Symbol(pino.levelVal)]: 30
    }
  },
  profiler: DummyRow { action: DummyAction {} },
  params: {},
  subdomains: {},
  route: {
    pattern: '/',
    handler: 'HomeController.index',
    meta: {
      namespace: undefined,
      resolvedHandler: [Object],
      resolvedMiddleware: [],
      finalHandler: [AsyncFunction (anonymous)]
    },
    middleware: [],
    name: undefined
  },
  routeKey: 'GET-/'
}
<ref *1> HttpContext {
  request: Request {
    request: IncomingMessage {
      _readableState: [ReadableState],
      _events: [Object: null prototype],
      _eventsCount: 1,
      _maxListeners: undefined,
      socket: [Socket],
      httpVersionMajor: 1,
      httpVersionMinor: 1,
      httpVersion: '1.1',
      complete: true,
      rawHeaders: [Array],
      rawTrailers: [],
      aborted: false,
      upgrade: false,
      url: '/',
      method: 'GET',
      statusCode: null,
      statusMessage: null,
      client: [Socket],
      _consuming: false,
      _dumped: false,
      _parsedUrl: [Url],
      [Symbol(kCapture)]: false,
      [Symbol(kHeaders)]: [Object],
      [Symbol(kHeadersCount)]: 32,
      [Symbol(kTrailers)]: null,
      [Symbol(kTrailersCount)]: 0,
      [Symbol(RequestTimeout)]: undefined
    },
    response: ServerResponse {
      _events: [Object: null prototype],
      _eventsCount: 1,
      _maxListeners: undefined,
      outputData: [],
      outputSize: 0,
      writable: true,
      destroyed: false,
      _last: false,
      chunkedEncoding: false,
      shouldKeepAlive: true,
      _defaultKeepAlive: true,
      useChunkedEncodingByDefault: true,
      sendDate: true,
      _removedConnection: false,
      _removedContLen: false,
      _removedTE: false,
      _contentLength: null,
      _hasBody: true,
      _trailer: '',
      finished: false,
      _headerSent: false,
      _closed: false,
      socket: [Socket],
      _header: null,
      _keepAliveTimeout: 5000,
      _onPendingData: [Function: bound updateOutgoingData],
      req: [IncomingMessage],
      _sent100: false,
      _expect_continue: false,
      parent: [Response],
      [Symbol(kCapture)]: false,
      [Symbol(kNeedDrain)]: false,
      [Symbol(corked)]: 0,
      [Symbol(kOutHeaders)]: null
    },
    encryption: Encryption {
      options: [Object],
      separator: '.',
      base64: Base64 {},
      algorithm: 'aes-256-cbc',
      cryptoKey: <Buffer bc 30 df 58 48 03 4f c0 95 ed d6 e6 4a 99 00 8d 77 7b 49 79 01 58 73 48 53 20 b1 f0 86 bf b2 01>,
      verifier: [MessageVerifier]
    },
    config: {
      allowMethodSpoofing: false,
      subdomainOffset: 2,
      generateRequestId: false,
      trustProxy: [Function: trust],
      etag: false,
      jsonpCallbackName: 'callback',
      cookie: [Object]
    },
    requestBody: {},
    routeParams: {},
    requestData: {},
    originalRequestData: {},
    requestQs: {},
    rawRequestBody: null,
    lazyAccepts: null,
    parsedUrl: Url {
      protocol: null,
      slashes: null,
      auth: null,
      host: null,
      port: null,
      hostname: null,
      hash: null,
      search: null,
      query: null,
      pathname: '/',
      path: '/',
      href: '/'
    },
    ctx: [Circular *1],
    cookieParser: CookieParser {
      cookieHeader: 'adonis-session=s%3AeyJtZXNzYWdlIjoiY2t4aGhraDhjMDAwMHJlbXlmMHNyM3Y0MSIsInB1cnBvc2UiOiJhZG9uaXMtc2Vzc2lvbiJ9.xEFgf2-zVXI-VvkowvV0OWR0-qh_zGRzKHBe_bwN2t4; ckxhhkh8c0000remyf0sr3v41=e%3AikN-cjr6SKQmKZvHXjzP3WwtMZRI1CqpJKWkyMBbZNEAJW7WOyGdt14GsoeH9UwNl0WFLj2Vk0YqaNK08rsvjg.cnhERzNiWThNT2ZTVFFVaA.MzgQT9bk2PasjTFTt7yhOccN6fTigUd3yF_nd-mwNdU',
      encryption: [Encryption],
      client: [CookieClient],
      cachedCookies: [Object],
      cookies: [Object]
    },
    __raw_files: {}
  },
  response: <ref *2> Response {
    request: IncomingMessage {
      _readableState: [ReadableState],
      _events: [Object: null prototype],
      _eventsCount: 1,
      _maxListeners: undefined,
      socket: [Socket],
      httpVersionMajor: 1,
      httpVersionMinor: 1,
      httpVersion: '1.1',
      complete: true,
      rawHeaders: [Array],
      rawTrailers: [],
      aborted: false,
      upgrade: false,
      url: '/',
      method: 'GET',
      statusCode: null,
      statusMessage: null,
      client: [Socket],
      _consuming: false,
      _dumped: false,
      _parsedUrl: [Url],
      [Symbol(kCapture)]: false,
      [Symbol(kHeaders)]: [Object],
      [Symbol(kHeadersCount)]: 32,
      [Symbol(kTrailers)]: null,
      [Symbol(kTrailersCount)]: 0,
      [Symbol(RequestTimeout)]: undefined
    },
    response: ServerResponse {
      _events: [Object: null prototype],
      _eventsCount: 1,
      _maxListeners: undefined,
      outputData: [],
      outputSize: 0,
      writable: true,
      destroyed: false,
      _last: false,
      chunkedEncoding: false,
      shouldKeepAlive: true,
      _defaultKeepAlive: true,
      useChunkedEncodingByDefault: true,
      sendDate: true,
      _removedConnection: false,
      _removedContLen: false,
      _removedTE: false,
      _contentLength: null,
      _hasBody: true,
      _trailer: '',
      finished: false,
      _headerSent: false,
      _closed: false,
      socket: [Socket],
      _header: null,
      _keepAliveTimeout: 5000,
      _onPendingData: [Function: bound updateOutgoingData],
      req: [IncomingMessage],
      _sent100: false,
      _expect_continue: false,
      parent: [Circular *2],
      [Symbol(kCapture)]: false,
      [Symbol(kNeedDrain)]: false,
      [Symbol(corked)]: 0,
      [Symbol(kOutHeaders)]: null
    },
    encryption: Encryption {
      options: [Object],
      separator: '.',
      base64: Base64 {},
      algorithm: 'aes-256-cbc',
      cryptoKey: <Buffer bc 30 df 58 48 03 4f c0 95 ed d6 e6 4a 99 00 8d 77 7b 49 79 01 58 73 48 53 20 b1 f0 86 bf b2 01>,
      verifier: [MessageVerifier]
    },
    config: {
      allowMethodSpoofing: false,
      subdomainOffset: 2,
      generateRequestId: false,
      trustProxy: [Function: trust],
      etag: false,
      jsonpCallbackName: 'callback',
      cookie: [Object]
    },
    router: Router {
      encryption: [Encryption],
      routeProcessor: [Function (anonymous)],
      routes: [],
      BriskRoute: [Function],
      RouteGroup: [Function],
      RouteResource: [Function],
      Route: [Function],
      RouteMatchers: [Function],
      matchers: RouteMatchers {},
      paramMatchers: {},
      lookupStore: [LookupStore],
      store: [Store],
      openedGroups: []
    },
    headers: {},
    explicitStatus: false,
    writerMethod: 'endResponse',
    cookieSerializer: CookieSerializer {
      encryption: [Encryption],
      client: [CookieClient]
    },
    hasLazyBody: false,
    lazyBody: [],
    ctx: [Circular *1]
  },
  logger: Logger {
    config: {
      name: 'hello-world',
      enabled: true,
      level: 'info',
      prettyPrint: true
    },
    pino: EventEmitter {
      trace: [Function: noop],
      debug: [Function: noop],
      info: [Function: LOG],
      warn: [Function: LOG],
      error: [Function: LOG],
      fatal: [Function (anonymous)],
      [Symbol(pino.serializers)]: [Object: null prototype],
      [Symbol(pino.formatters)]: [Object],
      [Symbol(pino.chindings)]: ',"pid":7807,"hostname":"broch-pc","name":"hello-world"',
      [Symbol(pino.levelVal)]: 30
    }
  },
  profiler: DummyRow { action: DummyAction {} },
  params: {},
  subdomains: {},
  route: {
    pattern: '/',
    handler: 'HomeController.index',
    meta: {
      namespace: undefined,
      resolvedHandler: [Object],
      resolvedMiddleware: [],
      finalHandler: [AsyncFunction (anonymous)]
    },
    middleware: [],
    name: undefined
  },
  routeKey: 'GET-/'
}

```

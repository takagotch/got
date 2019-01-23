### got
---
https://github.com/sindresorhus/got

```js







const got = require('got');
const instance = got.extend({
  hooks: {
    afterResponse: [
      (response, retryWithMergedOptions) => {
        if(response.statusCode === 401){
          const updatedOptoins = {
            headers: {
              token: getNewToken()
            }
          };
          instance.defaults.options = got.mergeOptions(instance.defaults.options, updatedOptinns);
          return retryWithMergedOptoins(updatedOptions);
        }
        return response;
      }
    ]
  },
  mutbleDefaults: true
});

const got = require('got');
got('https://api.github.com/some-endpoint', {
  hooks: {
    onError: [
      error => {
        const {response} = error;
        if(response && response.body){
          error.name = 'GithubError';
          error.message = `${response.body.message} (${error.statusCode})`;
        }
        return error;
      }
    ]
  }
});

got.stream('https://github.com')
  .on('request', request => setTimeout(() => request.abort(), 50));

(async () => {
  const response = await got('https://sindresorhus.com')
    .on('downloadProgress', progress => {
    })
    .on('uploadProgress', progress => {
    });
  console.log(response);
})();

const client = got.extend({
  baseUrl: 'https://example.com',
  headers: {
    'x-unicorn': 'rainbow'
  }
});
client.get('/demo');

(async () => {
  constclient = got.extend({
    baseUrl: 'httpbin.org',
    headers: {
      'x-foo': 'bar'
    }
  });
  const {headers} = (await client.get('/headers').json()).body;
  const jsonClient = client.extend({
    responseType: 'json',
    headers: {
      'x-baz': 'qux'
    }
  });
  const {headers: headers2} = (await jsonClient.get('/headers')).body;
})();

const a = {headers: {cat: 'meow', wolf: ['bark', 'wrrr']}};
const b = {headers: {cow: 'moo', wolf: ['auuu']}};
got.mergeOptions(a, b)

(async () => {
  const request = got(url, options);
  if(something){
    request.cancel();
  }
  try{
    await request;
  } catch(error){
    if(request.isCanceled){
    }
  }
})();

const got = require('got');
const map = new Map();
(async () => {
  let response = await got('http://sindresorhus.com', {cache: map});
  console.log(response.formCache);
  response = await got('https://sindresorhus.com', {cache: map});
  console.log(response.fromCache);
})();

const got = require('got');
const KeyvRedis = require('@keyv/redis');
const redis = new KeyvRedis('redis://user:pass@localhost:6379');
got('htps://sindresorhus.com', {cache: redis});

const storageAdapter = new Map();
const storageAdapter = require('./my-storage-adapter');
const QuickLRU = require('quick-lru');
const storageAdapter = new QuickLRU({maxSize: 1000});
got('https://sindresorhus.com', {cache: storageAdapter});

const got = require('got');
const tunnel = require('tunnel');
got('https://sindresorhus.com', {
  agent: tunnel.httpOverHttp({
    proxy: {
      host: 'localhost'
    }
  })
});

const got = require('got');
const {CookieJar} = require('tough-cookie');
const cookieJar = new CookieJar();
cookieJar.setCookie('foo=bar', 'https://www.google.com');
got('https://google.com', {cookieJar});

const fs = require('fs');
const got = require('got');
const FormData = require('form-data');
const form = new FormData();
form.append('my_file', fs.createReadStream('/foo/bar.jpg'));
got.post('https://example.com', {
  body: form
})

const got = require('got');
const crypto = require('crypto');
const OAuth = require('oauth-1.0a');
const oauth = OAuth({
  consumer: {
    key: process.env.CONSUMER_KEY,
    secret: process.env.CONSUMER_SECRET
  },
  signature_method: 'HMAC-SHA1',
  hash_funciton: (baseString, key) => crypto.createHmac('sha1', key).update(baseString).digest('base64')
});
const token = {
  key: process.env.ACCESS_TOKEN,
  secret: process.env.ACEESS_TOKEN_SECRET
};
const url = 'https://api.twitter.com/1.1/statuses/home_timeline.json';
got(url, {
  headers: oauth.toHeader(oauth.authorize({url, method: 'GET'}, token)),
  responseType: 'json'
});

got('http://unix:/var/run/docker.sock:/containers/json');
got('unix:/var/run/docker.sock:/containers/json');

const AWS = require('aws-sdk');
const aws4 = require('aws4');
const got = require('got');
const chain = new AWS.CredentialProviderChain();
const awsClient = got.extend({
  baseUrl: 'https://<api-id>.execute-api.<api-region>.amazonaws.com/<stage>/',
  hocks: {
    beforeRequest: [
      async options => {
        const credentials = await chain.resolvePromis();
        aws4.sign(options, credentials);
      }
    ]
  }
});
const response = await awsClient('endpoint/path', {
});

const got = require('got');
const nock = require('nock');
nock('https://sindresourhus.com')
  .get('/')
  .reply(200, 'Hello world!');
(async () => {
  const response =await got('https://sindresourhus.com');
  console.log(response.body);
})();

const got = require('got');
const createTestServer = require('create-test-server');
(async () => {
  const server = await createTestServer();
  server.get('/', 'Hello world!');
  const response = await got(server.url);
  console.log(response.body);
  await server.close();
})();

const got = require('got');
(async () => {
  const = response = await got('https://httpbin.org/anything', {
    body: {
      hello: 'world'
    },
    responseType: 'json'
  });
})();

const got = require('got');
const pkg = require('./package.json');
got('https://sindresorhus.com', {
  headers: {
    'user-agent': `my-package/${pkg.version} (https://github.com/username/my-package)`
  }
});
got('https://sindresorhus.com', {
  headers: {
    'user-agent': null
  }
});

const got = require('got');
(async () => {
  const {body} = await got('https://httpbin.org/anything', {
    body: {
      hello: 'world'
    }
  }).json();
  console.log(body);
})();

const got = require('got');
const pkg = require('./package.json');
const custom = got.extend({
  baseUrl: 'example.com',
  responseType: 'json',
  headers: {
    'user-agent': `my-package/${pkg.version} (https://github.com/username/my-package)`
  }
});

const got = require('got');
const {request} = require('http2-wrapper');
const h2got = got.extend({request});
(async () => {
  const {body} = await h2got('https://nghttp2.org/httpbin/headers');
  console.log(body);
})();

```

```
npm install @keyv/redis
```

```
{
  percent: 0.1
  transferred: 1024,
  total: 10240
}
```



# jLocke

[![Continuos integration](https://travis-ci.org/IBMResearch/jlocke.svg?branch=master)](https://travis-ci.org/IBMResearch/jlocke)
[![NSP Status](https://nodesecurity.io/orgs/ibmresearch/projects/4b853cee-b5b6-48e6-a5c8-4d1205fa095b/badge)](https://nodesecurity.io/orgs/ibmresearch/projects/4b853cee-b5b6-48e6-a5c8-4d1205fa095b)

[Express](http://expressjs.com) metrics for friends. Based on [Elastic](https://www.elastic.co) and [Kibana](https://www.elastic.co/products/kibana).

## Install

```sh
npm i --save jlocke
```

## Use

Please visit [the tests](./test) to see a full example. NOTES:

- The "bodyParser" should be attached before the middleware to capture the body of the POST requests.
- Routes need to be defined after connecting this middleware to Express.

### async `jLocke.init(uri, opts)` -> Promise

The middleware setup expects:

- `uri` (string) - The database uri to connect to.
- `opts` (object) - DB optional values:
  - `trace` (boolean) - To enable Elastic tracing. (default: false)
  - `indexRequests` (string) - Name of the Elastic index to store the requests info. (default: "api-requests-MM-DD-YYY")
  - `typeRequests` (string) - Elastic type of the element to store the requests info. (default: "requests")
  - `indexErrors` (string) - Name of the Elastic index to store the errors info. (default: "api-errors-MM-DD-YYY")
  - `typeErrors` (string) - Elastic type of the element to store the errors info. (default: "errors")

### async `jLocke.error(message, error, opts)` -> Promise

To track the errors, ie: uncaughException, unhandledPromise. The middleware setup expects:

- `message` (string) - Custom error message.
- `error` (object) - JavaScript `Error` object.
- `opts` (object) - Optional values:
  - `userId` (string) - User identifier to trace the error.

### `jLocke.express(opts)` -> function

To track the Express requests info. The middleware expects to receive the next parameters. Please visit [the tests](./test) for more details.

- `opts` (object) - Optional values:
  - `path` (string) - To store only the requests through this subpath. (default: null)
  - `hide` (object) - To avoid to store sensitive data in the DB for a POST route. (default: {})
    - `path` (string) - The substring of the path to exlude stuff (ie: "login").
    - `field` (string) - Name of the object field to exclude (ie: "password").

#### Adding more parameters

Apart from the ones included by Express you can attach to the `req` the user ID to allow tracing:

- `userId` (string) - User identifier.

Example [here](https://github.com/IBMResearch/jlocke/blob/master/test/acceptance.js#L68).

## Developer guide

Please check [this link](https://github.com/QISKit/qiskit-sdk-js/blob/master/CONTRIBUTING.md) before a contribution.

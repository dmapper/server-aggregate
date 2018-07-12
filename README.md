## server-aggregate

Racer server aggregate plugin. It allows only server-defined aggregate queries.

### install

With [npm](https://npmjs.org) do:

```
npm install server-aggregate
```

### usage

In our client code:

```js
require('server-aggregate/client')
```

On the server:
```js

const serverAggregate = require('server-aggregate')
serverAggregate(backend)  

// function addServerQuery accept
// 'collection' - collection name
// 'queryName'  - name of query
// 'cb' - function that accepts 'params' and 'shareRequest'
// and returns a query-object or error-string

backend.addAggregate('items', 'main', async (params, shareRequest) => {
  // ...
  // access control or whatever
  // ...
  
  return [
    {$match: {type: 'wooden'}}
  ]
})


```

Using queries (on the client):

```js
  // function serverQuery accepts 3 arguments:
  // 'collection' - collection name (should match one from addServerQuery)
  // 'queryName' - name of query (should match one from addServerQuery)
  // 'params' - object with query-params
  
  const query = model.aggregateQuery('items', 'main', {
    type: 'global'
  })

  model.subscribe(query, function(){
    // ...
  })
  
```

Alternative approach (using regular model.query)

```js
  // function serverQuery accepts 3 arguments:
  // 'collection' - collection name (should match one from addServerQuery)
  
  const query = model.query('items', {
    $aggregationName: 'main',
    $params: {
      type: 'global'
    }
  })

  model.subscribe(query, function(){
    // ...
  })
  
```

## MIT License
Copyright (c) 2018 by Artur Zayats


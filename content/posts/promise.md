---
title: "Promise"
date: 2022-06-09T20:39:58+08:00
draft: true
---

## Promise

What

A Proxy for a value that will eventually become availabel.

Why

deal with asyncchronous code without stuck in callback hell.

How

pending state, resolved state, rejected state.

### Promisifying

```javascript
const fs = require('fs')

const readFile = filename => {
  return new Promise((resolve, reject) => {
    fs.readFile(filename, (err, data) => {
      if (err) {
        reject(err)
        return
      }
      resolve(data)
    })
  })
}

readFile('/etc/hosts')
  .then(data => console.log(data))
  .catch(err => console.log(err))
```

### chaining Promises

```javascript
fetch('https://log-manager-api.htj.pdd.net/review/list?status=NOT_SUBMITTED&app=c')
  .then(res => {
    console.log('res: ', res);
    if(res.status >=200 && res.status < 300) {
      return Promise.resolve(res)
    }
    return Promise.reject(new Error(res.statusText))
  })
  .then(res => res.json())
  .then(res => {
    console.log(res);
  })
  .catch(error => {
    console.log('Request failed', error)
  })
```

### promise api

Promise.all()

Promise.any()

Promise.race()

### async/await

to reduce the boilerplate around promises

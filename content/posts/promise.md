---
title: "Promise"
date: 2022-06-09T20:39:58+08:00
draft: false
---

## Promise

*本文的主题是JavaScript的**Promise** API，试图在一篇文章内厘清这个开发中必不可少会经常用到的API。*

### 是什么

> A Proxy for a value that will eventually become availabel.
[来源](https://nodejs.dev/learn/understanding-javascript-promises)

对于已经了解Promise的开发者来说，这个英文的定义非常清晰简洁，但对完全不了解的人来说，可能会一头雾水，我尝试给这部分朋友解释下：Promise本质上是一个值的代理，当这个值变得可用时，代理会告诉你这个值可用了，不需要你（进程）一直盯着这个值。

### 为什么要引入这个概念

> deal with asyncchronous code without stuck in callback hell.
[来源](https://nodejs.dev/learn/understanding-javascript-promises)

避免开发中处理异步的代码陷入回调地狱。

年轻的开发者可能对回调地狱没什么概念，在没有Promise的时代，处理异步请求只能通过回调函数，在NodeJs的API里还能窥见一些封建残余，这里拿fs（file system）模块为例

```javascript

const fs = require('fs');

fs.readFile('/ets/hosts', (err, data) => {
  if (err) throw err;
  // do something with data...
})

```

如果业务复杂到一定程度，代码里会出现很多回调的嵌套，使得项目异常难以维护。

### 实现原理

一个Promise包含三种状态

- pending state
- resolved state
- rejected state

对应到现实中，一件事，要么正在处理，要么处理完了，要么在处理的过程中出了差错。

比如你去饭店吃饭，点了一个大盘鸡，从下单开始，状态就是（pending），等了10分钟后，服务员把一盘热气腾腾大盘鸡端上桌了，此时状态就是（resolved），假如在你下单后，后厨发现没鸡了，服务员过来告诉你大盘鸡做不了，这就叫（rejected）。下单这个动作，可以理解为创建了一个Promise，之后无论大盘鸡做好没做好，服务员都会来通知你，最后要么你顺利吃上大盘鸡，要么吃不上，就这两种结果。

### Promisifying

那么，如何把本来需要借助回调的方法变成一个Promise呢，这个过程就被称为Promise化（Promisifying）

还是以fs API为例

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

### Promises链

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

### Promise API

Promise.all()

Promise.any()

Promise.race()

### async/await

to reduce the boilerplate around promises

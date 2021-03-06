---
title: .run
category: Navalia
order: 2
---

The run method is used to queue jobs. The run function simply takes a `function` that will be called with one argument: `chrome` which is an instance of `Chrome`, and contains the browser-api. This method also takes care of cleanup, so there's no need to call any done methods in this workflow.

> Run will return a promise if you need to do further orchestration, or react to a job that has completed.

*JavaScript*
```js
const { Navalia } = require('navalia');
const navalia = new Navalia();

navalia
  .run((chrome) => chrome.navigate('http://joelgriffith.net'))
  .then(() => console.log('Page visited!'));
```

*TypeScript*
```ts
import { Navalia } from 'navalia';
const navalia:Navalia = new Navalia();

async function visitPages() {
  await navalia.run(async (chrome) => chrome.navigate('http://joelgriffith.net'));
  console.log('Complete!');
}

visitPages();
```

> You can also run multiple jobs in parallel.

*JavaScript*
```js
const { Navalia } = require('navalia');
const navalia = new Navalie();

navalia.run((chrome) => {
  return chrome.navigate('http://joelgriffith.net');
});

navalia.run((chrome) => {
  return chrome.navigate('https://news.ycombinator.net');
});
```

*TypeScript*
```ts
import { Navalia } from 'navalia';
const navalia:Navalia = new Navalia();

navalia.run(async (chrome) => {
  return chrome.navigate('http://joelgriffith.net');
});

navalia.run(async (chrome) => {
  return chrome.navigate('https://news.ycombinator.net');
});
```

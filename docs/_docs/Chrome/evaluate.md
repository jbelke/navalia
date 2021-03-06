---
title: .evaluate
category: Chrome
---

The async `evaluate` method accepts a function, and an optional set of arguments, to run inside of the Chrome JavaScript evironment. It's important to highlight that any arguments or other references _must_ be passed in as an argument (things like closures won't work). This is due to the fact that the function gets injected into the Chrome runtime, which requires everything to be serialzed.

Evaluate returns the result of the function, or throws if there's an issue.

> You can also execute async functions. Navalia will handle them as long as they return a 'then`-able

*JavaScript*
```js
const { Chrome } = require('navalia');
const chrome = new Chrome();

chrome.goto('https://www.google.com')
.then(() => chrome.evaluate(() => window.location.href))
.then((result) => console.log(result)); // Prints `https://www.google.com`
```

*TypeScript*
```ts
import { Chrome } from 'navalia';
const chrome = new Chrome();

await chrome.goto('https://www.google.com');
const res = await chrome.evaluate(() => window.location.href);
console.log(res);  // Prints `https://www.google.com`
```

Using arguments is pretty simple as well:

*JavaScript*
```js
const { Chrome } = require('navalia');
const chrome = new Chrome();

function getInnerText(selector) {
  return document.querySelector(selector).text;
}

chrome.goto('https://www.google.com')
.then(() => chrome.evaluate(getInnerText, 'title'))
.then((result) => console.log(result)); // Prints `Google`
```

*TypeScript*
```ts
import { Chrome } from 'navalia';
const chrome = new Chrome();

function getInnerText(selector):string {
  return document.querySelector(selector).text;
}

async function evaluate() {
  await chrome.goto('https://www.google.com');
  const res = await chrome.evaluate(getInnerText, 'title');
  console.log(res);  // Prints `https://www.google.com`
}

evaluate();
```

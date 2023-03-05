---
layout: default
title: Creating Promises
nav_order: 2
parent: Promises
grand_parent: ES6
---

## Creating Promises

Promise는 비동기 작업이 맞이할 미래의 완료 또는 실패와 그 결과값을 나타낸다. 따라서 Promise를 만들 때는 실행할 수 있는 함수를 넣어주어야 한다.

```js
const getData = new Promise((resolve, reject) => {
  setTimeout(resolve, 3000, "resolved!");
});

console.log(getData);
setInterval(console.log, 1000, getData);
```

{: .highlight }

> Promise {&lt;pending&gt;}<br/>
> Promise {&lt;pending&gt;}<br/>
> Promise {&lt;fulfilled&gt;: 'resolved!'}<br/>
> ...

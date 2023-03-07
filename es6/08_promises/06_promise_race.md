---
layout: default
title: Promise.race
nav_order: 6
parent: Promises
grand_parent: ES6
---

## Promise.race

Promise.race는 Promise.all과 사용법은 같다. 다른 점은 자식 Promises들중에 하나라도 resolve되거나 reject되면 된다.

```js
const p1 = new Promise((resolve) => {
  setTimeout(resolve, 500, "First");
});
const p2 = new Promise((resolve) => {
  setTimeout(resolve, 1000, "Second");
});
const p3 = new Promise((resolve) => {
  setTimeout(resolve, 300, "Third");
});

const racePromise = Promise.race([p1, p2, p3]);

racePromise
  .then((values) => console.log(values))
  .catch((error) => console.log(error));
```

{: .highlight }
Third

```js
const p1 = new Promise((resolve) => {
  setTimeout(resolve, 500, "First");
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(reject, 100, "Error: Second");
});
const p3 = new Promise((resolve) => {
  setTimeout(resolve, 300, "Third");
});

const racePromise = Promise.race([p1, p2, p3]);

racePromise
  .then((values) => console.log(values))
  .catch((error) => console.log(error));
```

{: .highlight }
Error: Second

resolve던 reject던 상관없이 가장 먼저 끝나는 값을 따르게 된다.

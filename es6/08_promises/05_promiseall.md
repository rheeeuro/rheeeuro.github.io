---
layout: default
title: Promise.all
nav_order: 5
parent: Promises
grand_parent: ES6
---

## Promise.all

Promise.all는 주어진 모든 Promise를 실행한 후 진행되는 하나의 Promise를 반환한다. 하나의 API가 아닌 여러 개의 API에서 값을 받아올 경우 유용하다.

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

const motherPromise = Promise.all([p1, p2, p3]);

motherPromise.then((values) => console.log(values));
```

{: .highlight }
(3) ['First', 'Second', 'Third']

Promise.all이 다른 Promise들이 전부 실행될 때까지 기다렸다가 진행된다. 따라서 나오는 값들도 Array가 된다.
각각의 Promise를 따로 기다렸다가 Array에 넣어주는 경우 순서가 뒤바뀔 수도 있지만, Promise.all은 값의 순서를 보존해준다.

---

```js
const p1 = new Promise((resolve) => {
  setTimeout(resolve, 500, "First");
});
const p2 = new Promise((resolve, reject) => {
  setTimeout(reject, 1000, "Error: Second");
});
const p3 = new Promise((resolve) => {
  setTimeout(resolve, 300, "Third");
});

const motherPromise = Promise.all([p1, p2, p3]);

motherPromise
  .then((values) => console.log(values))
  .catch((error) => console.log(error));
```

{: .highlight }
Error: Second

Promise.all의 자식 Promise중에 하나라도 reject되는 경우 Promise.all도 reject된다.

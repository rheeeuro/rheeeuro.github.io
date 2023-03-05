---
layout: default
title: Using Promises
nav_order: 3
parent: Promises
grand_parent: ES6
---

## Using Promises

promise를 사용하기 위해서는 명령이 끝나고 값을 반환하기 위해 then을 사용해야 한다.

```js
const getData = new Promise((resolve, reject) => {
  setTimeout(resolve, 3000, "resolved!");
});

getData.then((value) => console.log(value));
```

{: .highlight }
resolved!

---

만약 resolve가 아닌 reject를 handling하려면 catch를 사용해야 한다.

```js
const getData = new Promise((resolve, reject) => {
  setTimeout(reject, 3000, "error!");
});

getData
  .then((value) => console.log(value))
  .catch((error) => console.log(error));
```

{: .highlight }
error!

then부분과 catch부분은 같이 실행되지 않는다. 하나가 실행되면 하나는 실행되지 않는다.

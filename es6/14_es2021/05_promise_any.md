---
layout: default
title: Promise any
nav_order: 5
parent: ES2021
grand_parent: ES6
---

## Promise any

Promise.all은 array 내의 promise들이 모두 완료된 뒤에 then이 실행된다. 하지만 Promise.any는 array 내의 promise들이 어느 하나라도 완료되면 then으로 넘어간다.

```js
const p1 = new Promise((resolve) => {
  setTimeout(resolve, 1000, "quick");
});
const p2 = new Promise((resolve) => {
  setTimeout(resolve, 5000, "slow");
});

Promise.all([p1, p2]).then(console.log);
```

{: .highlight }
(2) ['quick', 'slow']

```js
const p1 = new Promise((resolve) => {
  setTimeout(resolve, 1000, "quick");
});
const p2 = new Promise((resolve) => {
  setTimeout(resolve, 5000, "slow");
});

Promise.any([p1, p2]).then(console.log);
```

{: .highlight }
quick

API를 사용해 모든 데이터를 받아오려면 Promise.all을, 분석값이나 view를 카운트할 때, 혹은 API들이 비슷한 결과를 반환하는 경우 Promise.any를 사용한다.

reject의 경우 Promise.any는 어느 하나를 기다리기 때문에 둘다 에러가 나는 경우 두 개의 에러를 출력한다.

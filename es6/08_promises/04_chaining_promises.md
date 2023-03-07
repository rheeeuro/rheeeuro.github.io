---
layout: default
title: Chaining Promises
nav_order: 4
parent: Promises
grand_parent: ES6
---

## Chaining Promises

다음과 같이 promise의 then도 chaining해서 사용할 수 있다.

```js
const getData = new Promise((resolve, reject) => {
  resolve(2);
});

getData
  .then((number) => {
    console.log(number);
    return number * 2;
  })
  .then((number) => {
    console.log(number);
    return number * 2;
  })
  .then((number) => {
    console.log(number);
    return number * 2;
  })
  // catch도 사용 가능
  .catch((error) => console.log(error));
```

{: .highlight }

> 2
>
> 4
>
> 8

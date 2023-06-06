---
layout: default
title: Promise allSettled
nav_order: 8
parent: ES2020
grand_parent: ES6
---

## Promise allSettled

Promise allSettled는 Promise all과 다르다. Promise.all은 안의 array에 있는 모든 promise들이 성공하면 response를 반환하고 array중 하나라도 에러를 낸다면 전체에 에러가 발생한다.

```js
const p = Promise.all([
  fetch("https://yts.mx/api/v2/list_movies.json"),
  fetch("https://yts.mx/api/v2/list_movies.json"),
  fetch(), // error
])
  .then((response) => console.log("success! ", response))
  .catch((e) => console.log("error: ", e));
```

{: .warning }
error: TypeError: Failed to execute 'fetch' on 'Window': 1 argument required, but only 0 present.

Promise allSettled는 이와 달리 개별 promise의 결과를 오브젝트 형식으로 반환한다.

```js
const p = Promise.allSettled([
  fetch("https://yts.mx/api/v2/list_movies.json"),
  fetch("https://yts.mx/api/v2/list_movies.json"),
  fetch(), // error
])
  .then((response) => console.log("success! ", response))
  .catch((e) => console.log("error: ", e));
```

{: .highlight }

> success! (3) [{…}, {…}, {…}]
>
> 0:{status: 'fulfilled', value: Response}
>
> 1:{status: 'fulfilled', value: Response}
>
> 2:{status: 'rejected', reason: TypeError: Failed to execute 'fetch' on 'Window': 1 argument required, but only 0 present. at <…}

Promise allSettled는 에러와 상관없이 모든 promise가 끝나면 success를 반환한다.

모든 promise가 잘 작동되는지 확인하려면 Promise allSettled를 사용하고 모든 Promise가 동시에 동작하는지만 환인하려면 Promise.all을 사용하는 것이 좋다.

Promise all은 서로 상관이 있는 promise들을 동작시킬 때 사용하고 Promise allSettled는 promise들이 서로 상관이 없는 경우 사용하는것이 좋다.

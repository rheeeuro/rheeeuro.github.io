---
layout: default
title: Async Await
nav_order: 1
parent: Async/Await
grand_parent: ES6
---

## Async Await

Async와 Await는 Promise나 then, catch와 같은 것들을 보기 좋게 만들어준다. async/await은 기본적으로 Promise를 사용하는 코드를 더 좋아보이게 하는 문법이다. <br />
await는 항상 async 함수 안에서만 사용할 수 있다.

```js
const getMovies = async () => {
  const response = await fetch(
    "https://yts.mx/api/v2/list_movies.json?sort_by=download_count"
  );
  console.log(response);
};

getMovies();
```

{: .highlight }
Response {type: 'basic', url: 'https://yts.mx/api/v2/list_movies.json?sort_by=download_count', redirected: false, status: 200, ok: true, …}

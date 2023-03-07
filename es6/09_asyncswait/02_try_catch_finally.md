---
layout: default
title: Try Catch Finally
nav_order: 2
parent: Async/Await
grand_parent: ES6
---

## Try Catch Finally

다른 언어의 try/catch 문법처럼 async await에서도 에러를 캐치할 수 있다.

```js
const getMovies = async () => {
  try {
    const response = await fetch(
      "https://yts.mx/api/v2/list_movies.json?    sort_by=download_count"
    );
    const json = await response.json();
    console.log(json);
  } catch (error) {
    console.log(error);
  } finally {
    console.log("done");
  }
};

getMovies();
```

{: .highlight }

> TypeError: Failed to fetch
>
> done

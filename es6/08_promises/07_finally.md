---
layout: default
title: Finally
nav_order: 7
parent: Promises
grand_parent: ES6
---

## Finally

finally는 promise가 모두 완료된 뒤에 실행된다. resolve가 되던 reject가 되던 상관없이 finally가 실행된다.

```js
const p1 = new Promise((resolve) => {
  setTimeout(resolve, 500, "First");
})
  .then((value) => console.log(value))
  .catch((error) => console.log(error))
  .finally(() => console.log("done"));
```

{: .highlight }

> First
>
> done

보통 finally는 API를 호출한 뒤 로딩 화면이나 로딩 spinner를 멈추는 데에 사용된다.

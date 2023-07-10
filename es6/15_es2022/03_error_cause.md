---
layout: default
title: Error cause
nav_order: 3
parent: ES2022
grand_parent: ES6
---

## Error cause

Error.cause는 개발자의 DX를 위해 만들어졌다. Error의 두번째 parameter에 부가적인 정보를 담을 수 있다.

```js
try {
  2 + 2;
  throw new Error("DB Connection Failed.", {
    cause: "Password is incorrect.",
  });
} catch (e) {
  console.log(e.message, e.cause);
}
```

{: .highlight }

> DB Connection Failed.
>
> Password is incorrect.

cause는 꼭 문자열일 필요가 없고 아무 자료구조나 가능하다.

```js
try {
  2 + 2;
  throw new Error("DB Connection Failed.", {
    cause: {
      error: "Password is incorrect.",
      value: 1234,
      message: ["too short", "only number not ok"],
    },
  });
} catch (e) {
  console.log(e.cause);
}
```

Error.cause를 통해 더 나은 에러를 만들 수 있다.

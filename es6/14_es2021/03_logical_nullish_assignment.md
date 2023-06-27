---
layout: default
title: Logical NULLISH Assignment
nav_order: 2
parent: ES2021
grand_parent: ES6
---

## Logical NULLISH Assignment

Logical NULLISH Assignment(??=)는 logical OR assignment(||=)과 상당히 비슷하다

```js
const user = {
  username: "Tom",
  password: 123,
  isAdmin: false,
};

user.isAdmin ||= true;

console.log(user);
```

{: .highlight }
{username: 'Tom', password: 123, isAdmin: true}

하지만 logical nullish assignment는 값이 오직 null이나 undefined인 경우만 체크한다.

```js
const user = {
  username: "Tom",
  password: 123,
  isAdmin: false,
};

user.isAdmin ??= true;

console.log(user);
```

{: .highlight }
{username: 'Tom', password: 123, isAdmin: false}

Logical OR assignment는 애매한 부분이 많아 보통 logical NULLISH assignment를 사용한다.

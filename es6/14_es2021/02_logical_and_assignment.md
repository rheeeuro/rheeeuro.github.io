---
layout: default
title: Logical AND Assignment
nav_order: 2
parent: ES2021
grand_parent: ES6
---

## Logical AND Assignment

Logical AND assignment는 logical OR assignment와 완전히 반대이다. Logical OR assignment는 변수가 falsy인 경우 변수에 value를 넣어주는 것 이라면, logical AND assignment는 변수가 truthy인 경우 값을 넣어준다.

```js
const user = {
  username: "Tom",
  password: 123,
};

if (user.password) {
  user.password = "[secret]";
}

console.log(user);
```

{: .highlight }
{username: 'Tom', password: '\[secret\]'}

이런 경우에 logical AND assignment를 사용할 수 있다.

```js
const user = {
  username: "Tom",
  password: 123,
};

user.password &&= "[secret]";

console.log(user);
```

{: .highlight }
{username: 'Tom', password: '\[secret\]'}

다음과 같이 패스워드가 있는 경우 업데이트 해준다. 만약 존재하지 않는 값에 logical AND assignment를 사용하면 아무런 변화가 없게 된다.

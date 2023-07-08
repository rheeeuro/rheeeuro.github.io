---
layout: default
title: Object hasOwn
nav_order: 2
parent: ES2022
grand_parent: ES6
---

## Object hasOwn

오브젝트에는 이미 hasOwnProperty라는 메서드가 존재한다.

```js
const user = {
  name: "Tom",
};

console.log(user.hasOwnProperty("isAdmin"));
console.log(user.hasOwnProperty("name"));
```

{: .highlight }

> false
>
> true

하지만 hasOwn은 살짝 다르게 사용한다.

```js
const user = {
  name: "Tom",
};

console.log(Object.hasOwn(user, "name"));
console.log(user.hasOwnProperty("name"));
```

{: .highlight }

> true
>
> true

같은 방식으로 사용되지만 Object.hasOwn을 대체제로 사용하길 권장한다고 documentation에 나와있다.

또한 다음과 같은 방식으로도 property를 체크할 수 있다.

```js
const user = {
  name: "Tom",
};

console.log("name" in user);
```

{: .highlight }
true

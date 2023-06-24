---
layout: default
title: Logical OR Assignment
nav_order: 1
parent: ES2021
grand_parent: ES6
---

## Logical OR Assignment

assignment operator을 이해하기 위해 유저의 이름을 가져오는 코드를 작성해보겠다.

```js
const name = prompt("What is your name?");

console.log(`Hello ${name}`);
```

이 때 prompt 창에 이름을 입력하지 않는다면 null이 들어가 `Hello null`이 출력되게 된다. 이를 수정하는 코드를 작성한다.

```js
const name = prompt("What is your name?");
if (!name) {
  name = "anonymous";
}
console.log(`Hello ${name}`);
```

이것이 logical OR operator가 존재하는 이유이다. logical OR operator는 비어있거나 falsy한 변수에 값을 넣을 수 있게 해준다. 여기서 falsy하다는 것은 `비어있는 텍스트(""), null, undefined, false, 0`을 포함한다.

따라서 이 코드를 다음과 같이 수정할 수 있다.

```js
const name = prompt("What is your name?");
name ||= "anonymous";

console.log(`Hello ${name}`);
```

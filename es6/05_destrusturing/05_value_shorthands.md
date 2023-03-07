---
layout: default
title: Value Shorthands
nav_order: 5
parent: Destructuring
grand_parent: ES6
---

## Value Shorthands

value shorthands는 object의 key 값과 value 변수의 이름이 같은 경우 이를 생략할 수 있다는 것이다.

```js
const result = getResult();

// es6 이전
const data = {
  result: result,
};

// es6 이후
const data = {
  result,
};
```

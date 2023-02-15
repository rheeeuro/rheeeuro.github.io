---
layout: default
title: Template Literal
nav_order: 1
parent: Strings
grand_parent: ES6
---

## Template Literal

자바스크립트에서 변수를 가진 문자열을 쓰는 방법은 string과 변수를 더하는 방법이 있다. 하지만 이는 띄어쓰기를 고려해야 하고 `+`와 `"`를 많이 사용해야 한다. ES6에서는 이를 개선해 backtick으로 template literal을 표기할 수 있다.

```js
// 기존
const sayHi(name = "anonymous") => "Hi, " + name;

// template literal
const sayHi2(name = "anonymous") => `Hi, ${name}`;
```

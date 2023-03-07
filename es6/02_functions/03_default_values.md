---
layout: default
title: Default Values
nav_order: 3
parent: Functions
grand_parent: ES6
---

## Default Values

ES6에서 function에 한 가지 더 추가된 점은 인자의 초기값을 설정할 수 있게 된 것이다. 기존에는 함수에 인자가 주어지지 않는 경우를 조건문으로 확인할 필요가 있었지만 ES6부터는 간편하게 초기값을 설정할 수 있다.

```js
// 초기값을 설정하지 않은 경우
function sayHi(name) {
  return "Hi" + name;
}

console.log(sayHi());
```

{: .highlight }
Hi undefined

```js
// 초기값을 확인해 넣어준 경우
function sayHi(name) {
  return "Hi" + (name || "anonymous");
}

console.log(sayHi());
```

{: .highlight }
Hi anonymous

```js
// ES6 이후 초기값 설정
function sayHi(name = "anonymous") {
  return "Hi" + anonymous;
}
const sayHiArrow = (name = "anonymous") => "Hi" + anonymous;

console.log(sayHi());
```

{: .highlight }
Hi anonymous

초기값에는 변수도 설정 가능하다.

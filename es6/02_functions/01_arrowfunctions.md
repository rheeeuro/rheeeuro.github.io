---
layout: default
title: Arrow Functions
nav_order: 1
parent: Functions
grand_parent: ES6
---

## Arrow Functions

arrow function은 개선된 함수의 모습으로 대체재가 아닌 선택사항이다.

```js
// 기존의 함수 선언 (hoisting 적용)
function fn(arg) {
  return null;
}

// 익명함수 변수에 할당 (const fn2; 만 hoisting)
const fn2 = function (arg) {
  return null;
};

// 익명 arrow 함수 변수에 할당
const fn3 = (arg) => null;
```

---

기존의 함수 선언식에서 function, return 등을 생략할 수 있기 때문에 훨씬 더 직관적이고 보기 좋게 된다.

```js
const arr = [1, 2, 3];

// 기존
const arrPlus1 = arr.map(function (item) {
  return item + 1;
});

// arrow function 활용
const arrPlus2 = arr.map((item) => item + 2);
```

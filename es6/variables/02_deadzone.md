---
layout: default
title: Dead Zone
nav_order: 1
parent: Variables
grand_parent: ES6
---

## Dead Zone

let은 var과 달리 temporal dead zone이라는 개념을 가지고 있다.

```js
// var name; 이 첫번째 줄로 hoisting
(function () {
  console.log(name);
  var name = "Tom";
})();
```

{: .highlight }
undefined

```js
(function () {
  console.log(name);
  let name = "Tom";
})();
```

{: .warning }
Uncaught ReferenceError: Cannot access 'name' before initialization

---

일반적으로 변수는 선언 - 초기화 - 할당 순서의 라이프사이클을 가진다. var은 선언이 hoisting되어 선언과 undefined로의 초기화가 동시에 이루어져 참조시 undefined를 반환하지만, let은 선언과 undefined로의 초기화가 분리되어 사이에 TDZ가 생성되고, 이때 참조하면 ReferenceError가 발생한다.

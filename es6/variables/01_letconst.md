---
layout: default
title: Let and Const
nav_order: 1
parent: Variables
grand_parent: ES6
---

## Let and Const

ES6 이전에는 모든 변수 선언에 var을 이용했다.
하지만 여러 개발자들이 개발할 때 변수명의 중복이나 재정의를 막을 수 없었다.
따라서 흔히 사용하는 변수명(a, b, c, name, age, etc...)을 기피했다.

```js
// 변수의 재정의 가능
(function () {
  var name = "Tom";

  ...

  var name = "James";

  ...

})();
```

---

ES6 이후 나온 let은 변수의 재정의를 막기 때문에 값이 변하는 변수를 사용할때 var 대신 이용한다.

```js
// 변수의 재정의 불가능
(function () {
  let name = "Tom";

  ...

  let name = "James";

  ...

})();
```

{: .warning }
Uncaught SyntaxError: Identifier 'name' has already been declared

---

const는 변하지 않는 상수를 저장할 때 사용한다.

```js
// 상수에 새로운 값 할당 불가능
(function () {
  const name = "Tom";

  ...

  name = "James";

  ...

})();
```

{: .warning }
Uncaught TypeError: Assignment to constant variable.

---

하지만 const가 생각하는 것처럼 완전히 read-only variable은 아니다.

```js
// 오브젝트 내부는 변경 가능
(function () {
  const item = {
    index: 1
  };

  ...

  item.index = "James";

  ...

})();
```

---

일반적으로 되도록이면 const를 사용하도록 하고 값이 변경되는 경우에는 let을 사용하는 것이 좋다. var는 사용하지 않는 것이 좋다.

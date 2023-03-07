---
layout: default
title: Spread Applications
nav_order: 2
parent: Rest and Spread
grand_parent: ES6
---

## Spread Applications

spread를 활용하는 방법들을 소개한다.

```js
const first = ["Red", "Orange", "Yellow"];

const last = ["Navy", "Purple"];

console.log([...first, "Green", "Blue", ...last]);
```

{: .highlight }
(7) ['Red', 'Orange', 'Yellow', 'Green', 'Blue', 'Navy', 'Purple']

---

```js
const lastName = prompt("Last Name");

const user = {
  username: "euro",
  age: 28,
  // 기존 방식
  // lastName: lastName !== "" ? lastName : undefined

  // spread
  ...(lastName !== "" && lastName),
};
```

다음과 같이 spread를 활용할 경우 lastName이 입력되지 않았을 때, lastName이라는 key도 존재하지 않게 만들 수 있다.

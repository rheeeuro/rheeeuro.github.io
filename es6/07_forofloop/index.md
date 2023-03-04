---
layout: default
title: For Of Loop
parent: ES6
nav_order: 7
---

## For Of Loop

```js
const rainbow = ["Red", "Orange", "Yellow", "Green", "Blue", "Navy", "Purple"];

// es6 이전
for (let i = 0; i < rainbow.length; i++) {
  console.log(rainbow[i]);
}

// 다음과 같이 깔끔하게 표현할 수 있지만 반복문을 중간에 멈출 수 없다는 단점이 있다.
rainbow.forEach((color) => console.log(color));

// es6 이후
for (const color of rainbow) {
  if (color === "Blue") {
    break;
  } else {
    console.log(color);
  }
}
```

---
layout: default
title: Swapping and Skipping
nav_order: 6
parent: Destructuring
grand_parent: ES6
---

## Swapping and Skipping

destructuring을 이용한 트릭에는 swapping과 skipping이 있다.

### Swapping

```js
let a = "b";
let b = "a";

[a, b] = [b, a];

console.log(a, b);
```

{: .highlight }
a b

다음과 같이 두 변수의 값을 서로 바꿀 경우 사용한다.

---

### Skipping

```js
const rainbow = ["Red", "Orange", "Yellow", "Green", "Blue", "Navy", "Purple"];

[, , , third, fourth] = rainbow;

console.log(third, fourth);
```

{: .highlight }
Green Blue

다음과 같이 array에서 특정 변수만 가져오고싶을 경우 사용한다.

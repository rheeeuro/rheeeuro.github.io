---
layout: default
title: Introduction to Spread
nav_order: 1
parent: Rest and Spread
grand_parent: ES6
---

## Introduction to Spread

spread는 기본적으로 array나 object를 풀어 헤치는 것이다.

```js
const arr = [1, 2, 3, 4];

console.log(arr, ...arr);
```

{: .highlight }
(4) [1, 2, 3, 4] 1 2 3 4

다음과 같이 두 개의 array를 풀어헤쳐 새로운 array를 만들 수도 있다.

```js
const arr1 = [1, 2, 3, 4];
const arr2 = ["a", "b", "c", "d"];

console.log([...arr1, ...arr2]);
```

{: .highlight }
(8) [1, 2, 3, 4, 'a', 'b', 'c', 'd']

object도 마찬가지로 적용해볼 수 있다.

```js
const obj1 = {
  name: "Tom",
  age: 28,
};
const obj2 = {
  gender: "Male",
  birthday: "1996.07.11",
};

console.log({ ...obj1, ...obj2 });
```

{: .highlight }
{name: 'Tom', age: 28, gender: 'Male', birthday: '1996.07.11'}

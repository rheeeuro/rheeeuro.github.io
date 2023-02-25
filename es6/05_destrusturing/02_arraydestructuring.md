---
layout: default
title: Array Destructuring
nav_order: 2
parent: Destructuring
grand_parent: ES6
---

## Array Destructuring

Array도 마찬가지로 destructuring을 할 수 있지만 object destructuring에 비해 활용도는 많이 낮은 듯 하다.

```js
const students = ["Tom", "Alex", "Brian", "Smith", ...]

// es6 이전
const first = students[0]
const second = students[1]
const third = students[2]

console.log(first, second, third);
```

{: .highlight }
Tom Alex Brian

```js
const students = ["Tom", "Alex", "Brian", "Smith", ...]

//es6 이후
const [first, second, third] = students;

console.log(first, second, third);
```

{: .highlight }
Tom Alex Brian

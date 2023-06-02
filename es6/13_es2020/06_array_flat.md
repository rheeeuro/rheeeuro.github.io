---
layout: default
title: Array flat
nav_order: 6
parent: ES2020
grand_parent: ES6
---

## Array flat

이전에는 다음과 같은 데이터를 통해 작업을 하려면 Underscore.js라는 라이브러리를 설치해 flatten이라는 함수를 이용해야 했다.

```js
[1, [2], [[8], [8], [[[8], [8], [[6], [5], [3]]]]]];
```

하지만 Array.flat을 통해 쉽게 해결할 수 있다. 인자로 depth를 넣어주면 된다.

```js
const arr = [1, [2], [[8], [8], [[[8], [8], [[6], [5], [3]]]]]];

console.log(arr.flat());
console.log(arr.flat(1));
console.log(arr.flat(2));
console.log(arr.flat(3));
console.log(arr.flat(4));
console.log(arr.flat(5));
```

{: .highlight }

> (5) [1, 2, Array(1), Array(1), Array(1)]
>
> (5) [1, 2, Array(1), Array(1), Array(1)]
>
> (5) [1, 2, 8, 8, Array(3)]
>
> (7) [1, 2, 8, 8, Array(1), Array(1), Array(3)]
>
> (9) [1, 2, 8, 8, 8, 8, Array(1), Array(1), Array(1)]
>
> (9) [1, 2, 8, 8, 8, 8, 6, 5, 3]

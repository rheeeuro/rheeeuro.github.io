---
layout: default
title: Numeric Separators
nav_order: 4
parent: ES2021
grand_parent: ES6
---

## Numeric Separators

자바스크립트에서 아주 큰 숫자를 사용하는 경우 underscore(`_`)를 넣으면 구분하기 쉬워진다. 이는 값을 변경시키지 않는다

```js
const total = 10_000_000_000_000_000_000;
console.log(total);
```

{: .highlight }
10000000000000000000

원한다면 아무 위치에나 쓸 수 있고 float형에도 사용할 수 있다. 다만 underscore(`_`)를 두 번 연속으로 사용하면 안된다.

```js
const total = 1_0_0_000_00_0000;
const floatTotal = 1_00_1.23_4;
console.log(total);
console.log(floatTotal);
```

{: .highlight }

> 100000000000
>
> 1001.234

```js
const total = 1__0_0_0;

console.log(total);
```

{: .warning }
Uncaught SyntaxError: Only one underscore is allowed as numeric separator

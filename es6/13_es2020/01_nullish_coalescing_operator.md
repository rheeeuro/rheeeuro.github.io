---
layout: default
title: ?? Operator
nav_order: 1
parent: ES2020
grand_parent: ES6
---

## ?? Operator (Nullish Coalescing Operator은)

Nullish Coalescing Operator은 `??`로 표시되며 logical OR (`||`)과 같은 논리연산자이다. 이 연산자는 기본값을 줄 때 매우 유용하다.

```js
let score;

console.log(`Score: ${score}`);
console.log(`Score: ${score || "NOT TESTED"}`);
```

{: .highlight }

> Score: undefined
>
> Score: NOT TESTED

이전에는 `||` 연산자를 사용했지만, 이 연산자는 기본적으로 boolean 기반이므로 다음과 같은 경우 의도하지 않은 방향으로 동작할 수 있다.

```js
let score = 0;

console.log(`Score: ${score || "NOT TESTED"}`);
```

{: .highlight }
Score: NOT TESTED

score 변수는 0으로 undefined가 아니지만 `||` 연산자는 boolean 기반이므로 변수가 boolean으로 변환되기 때문에 빈 문자열, 0과 같은 값인 경우 NOT TESTED가 뜨게 된다. 이럴 때 `??` 연산자를 사용하면 된다.

```js
let score = 0;

console.log(`Score: ${score ?? "NOT TESTED"}`);
```

{: .highlight }
Score: 0

`??` 연산자를 사용한 경우 score가 null 혹은 undefined일 때만 NOT TESTED가 출력되게 된다.

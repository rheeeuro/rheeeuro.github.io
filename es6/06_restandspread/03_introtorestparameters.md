---
layout: default
title: Intro to Rest Parameters
nav_order: 2
parent: Rest and Spread
grand_parent: ES6
---

## Intro to Rest Parameters

array를 풀어 헤치는 spread와 달리 rest는 각 인자를 array로 묶어준다.

```js
const ArgsParade = (...args) => console.log(args);

ArgsParade("a", "b", [1, 2, 3], true, 123);
```

{: .highlight }
(5) ['a', 'b', Array(3), true, 123]

이와 같이 rest를 활용할 수 있다.

```js
const printFirst = (first, ...rest) => console.log(first);

printFirst("a", "b", "c");
```

{: .highlight }
a

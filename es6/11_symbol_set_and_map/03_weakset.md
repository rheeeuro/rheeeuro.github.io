---
layout: default
title: WeakSet
nav_order: 3
parent: Symbol, Set and Map
grand_parent: ES6
---

## WeakSet

WeakSet은 기본적으로 Set과 동일하지만 오직 오브젝트만 저장할 수 있다.

```js
const weakSet = new WeakSet();
weakSet.add(1);
```

{: .warning }
Uncaught TypeError: Invalid value used in weak set

그리고 WeakSet은 size, entries, properties와 같은 메서드들이 존재하지 않고 add, delete, has만 존재한다.

또한 WeakSet은 이름 그대로 약하게 붙들려있기 때문에 참조되지 않는 WeakSet의 오브젝트는 가비지콜랙터에 의해 삭제된다.

```js
const weakSet = new WeakSet();
const first = { first: true };
weakSet.add(first);
weakSet.add({ second: true });

console.log(weakSet);
```

{: .highlight }

> before garbage collector: WeakSet {{…}, {…}}
>
> after garbage collector: WeakSet {{…}}

기본적으로 WeakSet은 잘 사용되지 않는다.

---
layout: default
title: Sets
nav_order: 2
parent: Symbol, Set and Map
grand_parent: ES6
---

## Sets

Set은 unique한 value를 저장할 수 있는 데이터 타입이다.

```js
const newSet = new Set([1, 2, 3, 3, 3, 4]);

console.log(newSet);
```

{: .highlight }
Set(4) \{1, 2, 3, 4\}

Set에도 다양한 메서드들이 존재한다.

```js
console.log(newSet.has(4));
console.log(newSet.has(6));

newSet.delete(1);
console.log(newSet);

newSet.clear();
console.log(newSet);

newSet.add("one");
console.log(newSet);
```

{: .highlight }

> true
>
> false
>
> Set(3) \{2, 3, 4\}
>
> Set(0) \{size: 0\}
>
> Set(1) \{'one'\}

```js
const newSet = new Set([1, 2, 3, 3, 3, 4]);

console.log(newSet.size);
console.log(newSet.keys());
```

{: .highlight }

> 4
>
> SetIterator \{1, 2, 3, 4\}

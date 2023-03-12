---
layout: default
title: Map and WeakMap
nav_order: 4
parent: Symbol, Set and Map
grand_parent: ES6
---

## Map and WeakMap

Map은 Set과 비슷하지만 Set은 value만 저장할 수 있는 한편 Map은 key value 형식으로 저장할 수 있다. Set과 같이 entries, has, get 등의 메서드가 존재한다.

```js
const newMap = new Map();

newMap.set("age", 20);
console.log(newMap);
```

{: .highlight }
Map(1) {'age' => 20}

---

WeakMap은 WeakSet과 같이 참조되지 않은 값은 가비지콜랙터의 대상이 된다.

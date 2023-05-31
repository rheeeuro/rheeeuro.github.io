---
layout: default
title: Obejct entries
nav_order: 5
parent: ES2020
grand_parent: ES6
---

## Obejct entries

오브젝트는 자바스크립트의 built-in 데이터 타입이다. 그 중 이번에는 Object enrties, Object values, Object fromEntries를 다뤄볼 예정이다.

```js
const person = {
  name: "Tom",
  age: 20,
};

// value만 얻고싶은 경우
console.log(Object.values(person));
// [key, value] 형태의 Array가 얻고싶은 경우
console.log(Object.entries(person));
```

{: .highlight }

> (2) ['Tom', 20]
>
> (2) [Array(2), Array(2)]
>
> > 0: (2) ['name', 'Tom']
> >
> > 1: (2) ['age', 20]
> >
> > length: 2
> > \[\[Prototype\]\]: Array(0)

Object fromEntries의 경우 Array로부터 object를 만들어준다.

```js
const obj = Object.fromEntries([
  ["name", "Tom"],
  ["age", 20],
  ["adult", true],
]);
console.log(obj);
```

{: .highlight }
`{name: 'Tom', age: 20, adult: true}`

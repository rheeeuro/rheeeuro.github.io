---
layout: default
title: Symbols
nav_order: 1
parent: Symbol, Set and Map
grand_parent: ES6
---

## Symbols

Symbol은 ES6에서 추가된 데이터 타입으로 uniqueness와 privacy라는 특성을 가지고있다.
Symbol은 description을 인자로 받는데 이 인자가 같더라도 같은 Symbol이 될 수 없다.

```js
const first = Symbol("number");
const second = Symbol("number");

console.log(first === second);
```

{: .highlight }
false

따라서 여러 사람이 큰 규모의 오브젝트에 key를 추가하는 경우 key의 이름이 중복되어 손실되는 사고를 방지할 수 있다.

```js
const obj = {
  result: {
    data: [1, 2, 3],
  },
};

obj["result"] = "result";

console.log(obj);
```

{: .highlight }
{result: 'result'}

```js
const obj = {
  [Symbol("result")]: {
    data: [1, 2, 3],
  },
};

obj[Symbol("result")] = "result";

console.log(obj);
```

{: .highlight }

> {Symbol(result): {…}, Symbol(result): 'result'}
>
> > Symbol(result): {data: Array(3)}
> >
> > Symbol(result): "result"
> >
> > [[Prototype]]: Object

이와 같이 key가 중복되는 경우에도 다른 key로 인식하게 된다.

---

또한 key로 불러올 때 반환되지 않아 privacy 측면에서 유리하다.

```js
const obj = {
  [Symbol("result")]: {
    data: [1, 2, 3],
  },
  hello: "hello",
};

console.log(Object.keys(obj));
```

{: .highlight }
['hello']

하지만 완전히 private하지는 않다. getOwnPropertySymbols 메서드를 통해 값을 받을 수 있다.

```js
const obj = {
  [Symbol("result")]: {
    data: [1, 2, 3],
  },
  hello: "hello",
};

console.log(Object.getOwnPropertySymbols(obj));
console.log(obj[Object.getOwnPropertySymbols(obj)[0]]);
```

{: .highlight }

> [Symbol(result)]
>
> {data: Array(3)}

다음과 같이 값도 다 불러올 수 있으므로 딱히 유용하지는 않은 것 같다.

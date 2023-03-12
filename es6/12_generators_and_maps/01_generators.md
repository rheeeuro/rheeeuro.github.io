---
layout: default
title: Generators
nav_order: 1
parent: Generators and Maps
grand_parent: ES6
---

## Generators

Generator는 기본적으로 일시정지(Pause)할 수 있는 함수이다. Generator를 사용하기 위해서는 function 뒤에 `*`을 붙여주어야 한다.

```js
function* list() {
  yield "first";
  yield "second";
  yield "third";
}

const listG = list();
console.log(list);
```

{: .highlight }
list {&lt;suspended&gt;}

yield는 기본적으로 return 이라고 보면 된다.
오브젝트가 suspended되었다고 나오는데 다음과 같이 순서대로 값을 오브젝트 형식으로 받아볼 수 있다.

```js
console.log(listG.next());
console.log(listG.next());
console.log(listG.next());
console.log(listG.next());
```

{: .highlight }

> {value: "fisrt", done: false}
> {value: "second", done: false}
> {value: "third", done: false}
> {value: undefined, done: true}

순서대로 값을 반환하고 done 여부를 같이 알려준다. 함수를 호출할 수는 있지만 이 이후로는 아무런 값을 받아볼 수 없다.

---

Generator는 usecase가 많지는 않지만, 다음과 같은 usecase가 존재한다.

```js
// yield 사이에 로직이 존재하는 경우
function* list() {
  ...
  yield "first";

  ...
  yield "second";

  ...
  yield "third";
}
```

```js
// array 반복문으로 yield하는 경우
const arr = ["first", "second", "third"];
function* list() {
  for (const item of arr) {
    yield item;
  }
}

const arrLooper = list();
```

Generator도 직접 사용하기보다는 다른 사람들이 만든 라이브러리에서 본다면 로직을 파악할 수 있을 것이다.

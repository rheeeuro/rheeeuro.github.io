---
layout: default
title: Introduction to Async
nav_order: 1
parent: Promises
grand_parent: ES6
---

## Introduction to Async

자바스크립트는 동시에 여러 일을 할 수 있다.

```js
const hello = fetch("http://example.com/movies.json");

console.log("something");
console.log(hello);
```

{: .highlight }

> something<br/>
> Promise {&lt;pending&gt;}<br/>
> GET http://example.com/movies.json net::ERR_FAILED

다음과 같이 데이터를 가져온 후 문자열을 출력하고 hello를 출력하라고 했지만 실제로는 문자열과 hello 이후 에러가 출력되는 모습이다. 이것을 자바스크립트의 비동기성(async)라고 한다.
자바스크립트는 데이터를 가져오는동안 프로그램의 실행을 멈추지 않는다.

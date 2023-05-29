---
layout: default
title: padStart and padEnd
nav_order: 3
parent: ES2020
grand_parent: ES6
---

## padStart and padEnd

시간을 표시한다고 가정해보자.

```js
let hours = 12;
let minutes = 3;
let seconds = 2;
console.log(`${hours}h:${minutes}m:${seconds}s`);
```

{: .highlight }
12h:3m:2s

이와 같은 식으로 하면 보기가 안좋으므로 한자리 수 인 경우에는 0을 붙여준다.

```js
console.log(`${hours}h:${minutes < 10 ? `0${minutes}` : minutes}m:${seconds}s`);
```

{: .highlight }
12h:03m:2s

다음과 같은 조건문을 시간, 분, 초에 모두 해 주어야 한다. 보통 이를 util로 따로 빼놓곤 하는데 이를 padStart로 해결할 수 있다.

```js
String(minutes).padStart(2, "0");
```

minutes가 2자리가 안될 경우 앞에 "0"을 채워 넣는다. 이 때 minutes는 number 자료형이기 때문에 string으로 변환해주어야 한다.

```js
console.log("5".padStart(5, "x"));
console.log("5".padEnd(5, "x"));

console.log("1".padStart(2, "0").padEnd(3, "s"));
```

{: .highlight }

> xxxx5
>
> 5xxxx
>
> 01s

padEnd도 같은 방식으로 사용할 수 있다. padStart와 padEnd는 앞과 뒤에 문자열을 채워주지만 원본 변수의 데이터는 바뀌지 않는다.

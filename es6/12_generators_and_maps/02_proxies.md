---
layout: default
title: Proxies
nav_order: 1
parent: Generators and Maps
grand_parent: ES6
---

## Proxies

Proxy는 일종의 필터 역할을 한다고 보면 된다. Proxy는 target과 handler를 인자로 받는다. handler에서는 get함수와 set함수를 선언해준다. 그리고 이 handler는 값을 변경하거나 조회할때 이것을 가로챈다.

```js
const user = {
  email: "rheeeuro@gmail.com",
  age: 28,
  password: "1234",
};

const userFilter = {
  get: () => {
    console.log("get something");
    return "Nothing";
  },
  set: () => {
    console.log("set something");
  },
};

const filteredUser = new Proxy(user, userFilter);

console.log(filteredUser.password);
```

{: .highlight }

> get something
>
> Nothing

---

get함수는 인자로 target, prop, receiver를 받는데 filteredUser.password를 조회한 경우 target은 user, prop은 password, receiver는 Proxy인 filteredUser가 된다.

```js
const userFilter = {
  get: (target, prop, receiver) => {
    return prop === "password" ? `${"*".repeat(5)}` : target[prop];
  },
  set: () => {
    console.log("set something");
  },
};

const filteredUser = new Proxy(user, userFilter);

console.log(filteredUser.age);
console.log(filteredUser.password);
```

{: .highlight }

> 28
>
> \*\*\*\*\*

handler에서는 get과 set 외에도 다양한 trap이 존재한다. <br/>
https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Proxy/Proxy

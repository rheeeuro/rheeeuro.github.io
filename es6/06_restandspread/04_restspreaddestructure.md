---
layout: default
title: Rest + Spread + Destructure
nav_order: 3
parent: Rest and Spread
grand_parent: ES6
---

## Rest + Spread + Destructure

rest와 spread, destructure를 다양하게 활용할 수 있다.

```js
const user = {
  name: "Tom",
  age: 28,
  password: "abc123",
};

const killPassword = ({ password, ...rest }) => rest;

const cleanedUser = killPassword(user);

console.log(cleanedUser);
```

{: .highlight }
{name: 'Tom', age: 28}

---

```js
const user = {
  name: "Tom",
  age: 28,
  password: "abc123",
};

const setCountry = ({ country = "KR", ...rest }) => ({ country, ...rest });

console.log(setCountry(user));
```

{: .highlight }
{country: 'KR', name: 'Tom', age: 28, password: 'abc123'}

---

```js
const user = {
  NAME: "Tom",
  age: 28,
  password: "abc123",
};

const rename = ({ NAME: name, ...rest }) => ({ name, ...rest });

console.log(rename(user));
```

{: .highlight }
{name: 'Tom', age: 28, password: 'abc123'}

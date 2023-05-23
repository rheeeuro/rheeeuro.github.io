---
layout: default
title: Optional Chaining
nav_order: 1
parent: ES2020
grand_parent: ES6
---

## Optional Chaining

Optional Chaining은 코드를 획기적으로 줄여줄 수 있다.

다음의 예시를 보자.

```js
const tom = {
  name: "Tom",
  profile: {
    age: 28,
    email: "tom1235@gmail.com",
  },
};

const james = {
  name: "James",
};

console.log(tom.profile.email);
console.log(james.profile.email);
```

{: .highlight }
tom1235@gmail.com

{: .warning }
Uncaught TypeError: Cannot read properties of undefined (reading 'email')

다음과 같이 API등에서 데이터를 받아온 경우 유저에게 profile 속성이 있는 줄 알고 코드를 짰더니 profile이 없는 유저가 있을 수 있다.

```js
// before optional chaining
console.log(james && james.profile && james.profile.email);
```

{: .highlight }
undefined

이런 경우 profile이 존재하는지 체크를 해주어야 하는데 이런 속성값이 많은 경우 아주 많은 코드를 작성해야 한다. 이같은 경우를 위해 Optional Chaining이 존재한다.

```js
console.log(james?.profile?.email);
```

{: .highlight }
undefined

Optional Chaining을 사용하면 속성값마다 `&&`를 붙여 체크해줘야 하던 번거로움을 한번에 해결할 수 있다.

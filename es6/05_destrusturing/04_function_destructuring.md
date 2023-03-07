---
layout: default
title: Function Destructuring
nav_order: 4
parent: Destructuring
grand_parent: ES6
---

## Function Destructuring

함수의 인자를 넘겨줄 때에도 destructuring이 유용하다.

```js
function setAccountOption(age, gender, notification, public, admin) {
  ...
}

...

setAccountOption(20, "Male", true, true, false)
```

다음과 같은 경우 true, true, true를 보고 어떤 값이 들어가는지 확인하기 힘들다.

```js
function setAccountOption(options) {
  if (!setting.notification) {
    ...
  }
  ...
}

...

setAccountOption({
  age: 20,
  gender:"Male",
  notification: true,
  public: true,
  admin: false
})
```

이를 개선해 object 형태로 넘겨주게 되면 함수 안에서 undefined여부를 확인해줘야 하는 번거로움이 생긴다.

```js
// es6 이후
function setAccountOption({age, gender, notification, public, admin = false}) {
  console.log(notification)
  ...
}

...

setAccountOption({
  age: 20,
  gender:"Male",
  notification: true,
  public: true,
  admin: false
})
```

이를 destructuring을 통해 간단명료하게 바꿀 수 있다.

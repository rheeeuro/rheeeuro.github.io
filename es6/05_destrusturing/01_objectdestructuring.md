---
layout: default
title: Object Destructuring
nav_order: 1
parent: Destructuring
grand_parent: ES6
---

## Object Destructuring

Destructuring은 object나 array, 그 외 요소들 안의 변수를 바깥으로 끄집어 내서 사용할 수 있도록 하는 것이다.

```js
// es6 이전
const setting = {
  notification: {
    follow: true,
    alert: true,
  },
};

if (setting.notification.alert) {
  // send alert

  ...

  // setting, notification, alert가 define되지 않았을 경우를 고려해야 한다.
}
```

```js
// es6 이후
const { notification } = setting; // notification을 const로 가져옴
const {
  notification: { alert },
} = setting; // alert를 const로 가져옴
const {
  notification: { follow = true },
} = setting; // 다음과 같이 선언되지 않았을 경우를 고려해 초기값 설정이 가능하다.
```

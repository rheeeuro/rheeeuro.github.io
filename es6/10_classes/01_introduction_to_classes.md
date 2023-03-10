---
layout: default
title: Introduction to Classes
nav_order: 1
parent: Classes
grand_parent: ES6
---

## Introduction to Classes

일반적으로 class는 다른 프로그래밍 언어의 class와 유사하다. 보통 직접 class를 만들어 사용하는 경우는 드물고 다른 이들이 만든 class를 가져다 사용하는 일이 많다. class를 이용하면 코드를 구조화하기 편리하다.

```js
class User {
  constructor(name) {
    this.username = name;
  }
  sayHi() {
    console.log(`Hi! I', ${this.username}`);
  }
}

const tom = new User("Tom");
const james = new User("James");

tom.sayHi();
james.sayHi();
```

{: .highlight }

> Hi! I', Tom
>
> Hi! I', James

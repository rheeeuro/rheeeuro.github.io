---
layout: default
title: Super
nav_order: 3
parent: Classes
grand_parent: ES6
---

## Super

다음과 같이 class를 상속받는 경우, 생성자를 만들게 되면 원래의 생성자를 잃게 된다.

```js
class User {
  constructor(name, password) {
    this.username = name;
    this.password = password;
  }
  sayHi() {
    console.log(`Hi! I', ${this.username}`);
  }
}

class Admin extends User {
  constructor(isSuperAdmin) {
    this.isSuperAdmin = isSuperAdmin;
  }
  manage() {
    console.log("manage website");
  }
}

const tom = new Admin(true);

tom.manage();
tom.sayHi();
```

{: .warning }
Uncaught ReferenceError: Must call super constructor in derived class before accessing 'this' or returning from derived constructor

다음과 같이 상속받은 클래스의 생성자에서 this를 사용하기 전 super constructor를 호출하라고 에러가 뜨는 것을 볼 수 있다. 그래서 다음과 같이 바꿀 수 있다.

```js
class User {
  constructor(name, password) {
    this.username = name;
    this.password = password;
  }
  sayHi() {
    console.log(`Hi! I', ${this.username}`);
  }
}

class Admin extends User {
  constructor(name, password, isSuperAdmin) {
    super(name, password);
    this.isSuperAdmin = isSuperAdmin;
  }
  manage() {
    console.log("manage website");
  }
}

const tom = new Admin("Tom", "1234", true);

tom.manage();
tom.sayHi();
```

{: .highlight }

> manage website
>
> Hi! I', Tom

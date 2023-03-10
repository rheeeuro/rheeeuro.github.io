---
layout: default
title: Extending Classes
nav_order: 2
parent: Classes
grand_parent: ES6
---

## Extending Classes

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
  manage() {
    console.log("manage website");
  }
}

const tom = new Admin("Tom", "1234");

tom.manage();
tom.sayHi();
```

{: .highlight }

> manage website
>
> Hi! I', Tom

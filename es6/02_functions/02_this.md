---
layout: default
title: This
nav_order: 2
parent: Functions
grand_parent: ES6
---

## This

일반 함수에서의 this는 함수를 호출한 객체를 바인딩하다.
따라서 일반 함수에서의 this는 함수를 호출한 window 객체, method나 생성자는 해당 함수를 보유한 객체를 가리키게 된다.

하지만 arrow function에서의 this는 lexical this로 상위 스코프의 this를 따라가게 된다.

```js
// <button>버튼</button> in HTML file
const button = document.querySelector("button");

// button 반환
button.addEventListener("click", function () {
  console.log(this);
});

// window 반환
button.addEventListener("click", () => {
  console.log(this);
});
```

{: .highlight }
`<button>버튼</button>`

{: .highlight }
Window {0: Window, window: Window, self: Window, document: document, name: '', location: Location, …}

일반 함수와 arrow function을 따로 선언하고 event listener에 등록해도 결과는 같다.

---

따라서 arrow function의 this는 callback함수에서 사용하기 편리하다. 일반 함수에서는 window를 가리키는데 반해 arrow function은 상위 객체를 따라가기 때문이다.

es6 이전에는 this는 별도의 변수에 할당해두는 등의 방법을 사용했지만 arrow function을 이용하면서 그런 번거로움이 줄었다.

---

하지만 arrow function도 사용함에 있어서 주의가 필요하다.
method, prototype, constructor 등에는 사용이 자제된다.

```js
const person = {
  name: "Tom",
  sayHi: () => console.log(`Hi ${this.name}`),
  sayHello() {
    console.log(`Hello ${this.name}`);
  },
};

person.sayHi();
person.sayHello();
```

{: .highlight }
Hi undefined

{: .highlight }
Hello Tom

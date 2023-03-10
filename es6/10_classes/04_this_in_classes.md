---
layout: default
title: This in Classes
nav_order: 3
parent: Classes
grand_parent: ES6
---

## This in Classes

다음과 같은 코드가 있다고 가정하자.

```html
<span id="number">0</span>
<button id="plusbutton">+</button>
<button id="minusbutton">-</button>
```

```js
class Counter {
  constructor({ initialNumber = 0, counterId, plusId, minusId }) {
    this.count = initialNumber;
    this.counterId = document.getElementById(counterId);
    this.plusBtn = document.getElementById(plusId);
    this.minusBtn = document.getElementById(minusId);
    this.addEventListeners();
  }
  addEventListeners() {
    this.plusBtn.addEventListener("click", this.increase);
    this.minusBtn.addEventListener("click", this.decrease);
  }
  increase() {
    this.count += 1;
    this.repaintCount();
  }
  decrease() {
    this.count -= 1;
    this.repaintCount();
  }
  repaintCount() {
    this.counter.innerText = this.count;
  }
}
```

플러스나 마이너스 버튼을 누른 경우 다음과 같은 에러가 나타난다.

{: .warning }
Uncaught TypeError: this.repaintCount is not a function

클래스에서 기본적으로 this는 생성되는 인스턴스를 가리키지만 버튼에서 이벤트 리스너를 등록하는 경우 this가 이벤트를 발생시킨 버튼이 되기 때문에 this.repaintCount가 없다고 나오는 것이다. 따라서 this를 클래스 인스턴스로 고정하고 싶은 경우 상위 스코프의 this를 따라가는 arrow function을 사용해야 한다.

```js
increase = () => {
  this.count += 1;
  this.repaintCount();
};
decrease = () => {
  this.count -= 1;
  this.repaintCount();
};
```

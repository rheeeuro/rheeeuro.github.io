---
layout: default
title: Callback
nav_order: 3
parent: Core JS
---

# Callback 함수

## Callback 함수란?
- callback 함수 (call/back): 회신되는 함수
- 함수의 제어권 위임 (해줘)
- 제어권 위임
  - 실행 시점
  - 매개변수
  - this

## 실행 시점

```js
var cb = function() {
  console.log("1초마다 실행");
};
setInterval(cb, 1000);
```

## 매개변수
```js
var arr = [1, 2, 3, 4, 5];
var entries = [];

arr.forEach(function(v, i) {
  entries.push([i, v, this[i]]);
  }, [10, 20, 30, 40, 50]);

console.log(entries);
// [[0, 1, 10], [1, 2, 20], [2, 3, 30], [3, 4, 40], [4, 5, 50]]
```


## this

```js
document.body.innerHTML = '<div id="a">abc</div>';
function cbFunc(x) {
  console.log(this, x);
}

document.getElementById('a').addEventListener('click', cbFunc);
// div, PointerEvent
```


## 콜백함수의 특징
- 다른 함수(A)의 인자로 콜백함수(B)를 전달하면, A가 B의 `제어권`을 갖게 된다.
- 특별한 요청(bind)이 없는 한, A에 `미리 정해놓은 방식`에 따라 B를 호출한다.
- 미리 정해놓은 방식이란 어떤 `시점`에 콜백을 호출할지, `인자`에는 어떤 값들을 지정할지, `this`에 무엇을 바인딜할지 등이다.

## 주의
callback은 함수이지 메서드가 아니다.

```js
var arr = [1, 2, 3, 4, 5];
var obj = {
  vals: [1, 2, 3],
  logValues: function(v, i) {
    if (this.vals) {
      console.log(this.vals, v, i);
    } else {
      console.log(this, v, i);
    }
  }
}

obj.logValues(1, 2); // 메서드로 호출
arr.forEach(obj.logValues); // 콜백함수로 전달 window, 1, 0
```

<details>
<summary>정답</summary>

```
[1, 2, 3], 1, 2
window, 1, 0
window, 2, 1
window, 3, 2
window, 4, 3
window, 5, 4
```
- 첫번째는 메서드로서 호출
- 두번쨰는 콜백함수로 호출

</details>
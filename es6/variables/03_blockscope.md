---
layout: default
title: Block Scope
nav_order: 3
parent: Variables
grand_parent: ES6
---

## Block Scope

let과 var의 또 다른 차이점은 Scope이다.

var은 Function Scope로 function 외부에서는 내부의 변수에 접근이 불가능하다.

```js
// var은 function 외부에서 접근 불가능

function a() {
  var name = "Tom";
}
console.log(name);
```

{: .warning }
Uncaught ReferenceError: name is not defined

---

하지만 let과 const는 Block Scope로 if, try, catch 등의 block의 외부에서도 접근이 불가능하다.

```js
// var은 block외부에서도 접근 가능

if (true) {
  var name = "Tom";
}
console.log(name);
```

{: .highlight }
Tom

```js
// let은 block외부에서 접근 불가능

if (true) {
  let name = "Tom";
}
console.log(name);
```

{: .warning }
Uncaught ReferenceError: name is not defined

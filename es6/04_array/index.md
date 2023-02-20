---
layout: default
title: Array
parent: ES6
nav_order: 4
---

## Array Method

### Array.of()

```js
const arr = Array.of("a", "b", "c", "d");

console.log(arr);
```

{: .highlight }
(4) ['a', 'b', 'c', 'd']

---

### Array.from()

```js
// 10 buttons in HTML file
const buttons = document.getElementByClassName("btn");
// HTMLCollection(10) [button.btn, button.btn, ...]

Array.from(buttons).forEach((button) =>
  button.addEventListener("click", () => {
    console.log("clicked");
  })
);
```

HTMLCollection과 같은 array-like object를 array로 바꿔준다.

---

### Array.prototype.find()

```js
const emails = [
  "dog@gmail.com",
  "cat@gmail.com",
  "duck@gmail.com",
  "mouse@gmail.com",
];
const result = emails.find((email) => email.includes("dog"));

console.log(result);
```

{: .highlight }
dog@gmail.com

인자 함수를 만족하는 첫번째 element를 반환한다.

---

### Array.prototype.findIndex()

```js
const emails = [
  "dog@gmail.com",
  "cat@gmail.com",
  "duck@gmail.com",
  "mouse@gmail.com",
];
const result = emails.findIndex((email) => email.includes("duck"));

console.log(result);
```

{: .highlight }
2

---

### Array.prototype.fill()

```js
const emails = [
  "dog@gmail.com",
  "cat@gmail.com",
  "duck@gmail.com",
  "mouse@gmail.com",
];
emails.fill("@", 1, 3);

console.log(emails);
```

{: .highlight }
(4) ['dog@gmail.com', '@', '@', 'mouse@gmail.com']

arr.fill(value[, start[, end]])

---
layout: default
title: HTML Fragments
nav_order: 2
parent: Strings
grand_parent: ES6
---

## HTML Fragments

string 안에 변수를 넣는 것 이외에도, template literal을 통해 html fragment를 나타낼 수 있다.

```js
const container = document.getElementById("container");
// 기존
const div = document.createElement("div");
const h1 = document.createElement("h1");
h1.innerText = "hi";
div.append(h1);
container.append(div);

// template literal
const hi = `
  <div>
    <h1>hi</h1>
  </div>
`;
container.innerHTML = hi;
```

---

또한 template literal은 모든 공백과 엔터를 고려한다.

```js
console.log(`

     h
    


         i
`);
```

{: .highlight }

```
h

         i
```

---

template literal을 통해 html을 깔끔한 코드로 추가 및 수정할 수 있다.

```js
const container = document.getElementById("container");
const arr = ["a", "b", "c", "d"];

const list = `
  <ul>
    ${arr.map((item) => `<li>${item}</li>`)}
  </ul>
`;
container.innerHTML = list;
```

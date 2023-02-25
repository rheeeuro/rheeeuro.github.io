---
layout: default
title: Renaming
nav_order: 3
parent: Destructuring
grand_parent: ES6
---

## Renaming

api 결과를 destructuring하는 경우 변수 이름이 마음에 들지 않을 수 있다. 이때 renaming을 통해 원하는 이름으로 변경할 수 있다.

```js
const setting = {
  theme: {
    primary_color: "#00b894",
  },
};

const {
  theme: { primary_color: primaryColor = "#0984e3" },
} = setting;

console.log(primaryColor);
```

{: .highlight }
#00b894

let을 사용하는 경우 트릭을 통해 미리 변수를 선언하고 나중에 값을 할당할 수도 있다.

```js
let primaryColor = "0984e3";

// 앞에 let이나 const를 붙이는 대신 전체를 괄호로 묶어준다.
({
  theme: { primary_color: primaryColor = "#0984e3" },
} = setting);

console.log(primaryColor);
```

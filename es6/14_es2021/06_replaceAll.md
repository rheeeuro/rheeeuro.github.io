---
layout: default
title: replaceAll
nav_order: 6
parent: ES2021
grand_parent: ES6
---

## replaceAll

replaceAll은 말 그대로 텍스트의 특정 문자열을 바꾸는 함수이다. replaceAll은 원래의 변수를 수정(mutate)하지 않는다.

```js
const text = "Tom Sam David";
const newText = text.replaceAll(" ", ", ");

console.log(newText);
console.log(text);
```

{: .highlight }

> Tom, Sam, David
>
> Tom Sam David

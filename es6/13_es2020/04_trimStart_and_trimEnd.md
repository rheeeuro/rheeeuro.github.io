---
layout: default
title: trimStart and trimEnd
nav_order: 4
parent: ES2020
grand_parent: ES6
---

## trimStart and trimEnd

trimStart는 기본적으로 자르는 기능이다. 비어있는 공간을 잘라준다.

```js
console.log("             hello".trimStart());
```

{: .highlight }
hello

반대로도 가능하다.

```js
console.log("             hello        ".trimEnd());
```

{: .highlight }
&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;hello

양쪽으로 자르고 싶다면 그냥 trim을 사용하면 된다.

```js
console.log("             hello        ".trim());
```

{: .highlight }
hello

주의해햐 할 점은 단어 사이의 공백은 없애주지 못하고, 변수 자체를 바꾸지는 않는다.

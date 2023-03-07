---
layout: default
title: String Method
nav_order: 3
parent: Strings
grand_parent: ES6
---

## String Method

ES6에서는 다양한 string method가 추가되었다.

### String.prototype.includes()

```js
const isEmail = (email) => email.includes("@");

console.log(isEmail("rheeeuro@gmail.com"));
```

{: .highlight }
true

---

### String.prototype.repeat()

```js
const list = "<li>item</li>\n".repeat(5);

console.log(list);
```

```<li>item</li>
<li>item</li>
<li>item</li>
<li>item</li>
<li>item</li>
```

---

### String.prototype.startsWith()

```js
const isUrl = (url) => url.startsWith("https://");

console.log(isUrl("https://github.com/rheeeuro"));
```

{: .highlight }
true

---

### String.prototype.endsWith()

```js
const isGmail = (url) => url.endsWith("@gmail.com");

console.log(isGmail("rheeeuro@gmail.com"));
```

{: .highlight }
true

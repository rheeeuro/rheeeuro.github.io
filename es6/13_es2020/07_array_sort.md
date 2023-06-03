---
layout: default
title: Array sort
nav_order: 7
parent: ES2020
grand_parent: ES6
---

## Array sort

array sort는 기본적으로 배열을 정렬해주는 기능이다.

```js
const arr = ["a", "c", "b"];
console.log(arr.sort());
```

{: .highlight }
(3) ['a', 'b', 'c']

하지만 자기만의 순서가 필요한 경우 비교함수를 만들어서 정렬해야 한다. 함수의 인자 `a, b`에서 `a가 작을 경우 음수`, `같을 경우 0`, `클 경우 양수`를 리턴하면 된다.

```js
const fruits = ["apple", "strawberry", "avocade"];

const sortFruitsByLength = (fruitA, fruitB) => {
  return fruitA.length - fruitB.length;
};

console.log(fruits.sort(sortFruitsByLength));
```

{: .highlight }
(3) ['apple', 'avocade', 'strawberry']

sort는 오브젝트를 정렬할 때 아주 유용하다.

```js
const people = [
  {
    name: "Tom",
    age: 20,
  },
  {
    name: "James",
    age: 25,
  },
];

const orderPeopleByAge = (personA, personB) => {
  return personA.age - personB.age;
};

console.log(people.sort(orderPeopleByAge));
```

{: .highlight }
(3) [{name: 'Tom', age: 20}, {name: 'James', age: 25}]

sort는 이전에 배운 다양한 함수와 달리 원본 array를 변경시킨다.

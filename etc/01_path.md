---
layout: default
title: Node.js path module
nav_order: 1
parent: Etc
---

## Node.js path module

Node.js에서 작업할 때 path 모듈을 자주 사용하게 되는데 의미는 대충 이해하지만 정확하게는 알지 못해 한번 정리해보려 한다.

### \_\_dirname, \_\_filename

`__dirname`과 `__filename`이 어디서 온건지 제대로 모르고 있었는데, node.js 자체에서 제공한다. `__dirname`은 실행 파일의 파일명을 제외한 경로가 반환되고, `__filename`은 실행 파일의 파일명을 포함한 경로가 반환된다.

```js
// file 명을 포함한 절대경로
console.log(__filename);

// file 명을 제외한 절대 경로
console.log(__dirname);
```

{: .highlight }
/Users/rheeeuro/Doc/directory.js

{: .highlight }
/Users/rheeeuro/Doc

변수의 결과는 운영체제마다 달라진다. Windows의 경우 구분자를 `\`로 사용하고, POSIX(macOS, Linux)의 경우 구분자로 `/`를 사용한다.

---

### Path Module

path 모듈은 Node.js 내장 모듈로 별도의 npm 설치과정이 필요없다.

- path.resolve([...path]): 전달된 인자를 오른쪽에서 왼쪽으로 읽으며 상대로와 절대 경로를 구분하고 절대경로를 만들어 반환한다.
- path.join([...paths]): 여러 인자를 넣으면 하나의 경로를 합쳐 반환하다. 상대경로를 표시하는 `..` 와 현 위치를 표시하는 `. `도 반영한 결과를 리턴한다.
- path.sep: 운영체제별 경로 구분자를 반환한다. Windows는 `\` , POSIX 는 `/` 값을 담고 있다.
- path.dirname(paths): 현재 파일이 위치한 폴더 경로를 보여준다.
- path.extname(paths): 현재 파일이 위치한 폴더 경로를 보여준다.
- path.normalize(path): `/` 나 `\` 를 실수로 여러번 사용했거나 혼용한 경우 정상적인 경로로 변환해준다.

---

### Windows 환경에서 `\\` 와 `\`를 같이 사용하는 경우

Windows에서 기본적으로 `\` 를 사용해 경로를 표시하는데, 자바스크립트에서 `\` 가 특수문자이기 때문에 `\`를 하나 더 붙여 `\\` 로 표기해야 한다. 예를 들어 `\n`은 자바스크립트에서 줄바꿈이라는 뜻이다. 따라서 `C:\node` 와 같은 경로에서 의도치 않은 오류가 발생할 수 있으므로 `C:\\node`로 표시한다.

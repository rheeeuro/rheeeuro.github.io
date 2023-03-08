---
layout: default
title: Introduction
nav_order: 1
parent: Electron
---

## Introduction

Electron은 HTML, CSS, Javascript로 Desktop app을 만들어주는 framework이다.
Chromuim과 Node.js가 내장되어있고, Javascript 코드 베이스로 Windows, macOS, Linux에 cross-platform app을 만들 수 있다.

나는 Electron을 들어는 보았지만 흥미가 생긴 것은 Steam의 Vampire Survivor가 Electron으로 만들었다는 사실을 알고난 이후부터이다. 군 복무 시절 HTML Canvas로 여러 게임을 만들어본 경험이 있기 때문에 그런 것들을 Desktop app으로 만들어보면 좋겠다는 생각을 했고, 그것들로 실습을 해볼 예정이다.

documentation의 기초 예제를 따라해보자.

```
npm install --save-dev electron
yarn add --dev electron
```

```js
// main.js

const { app, BrowserWindow } = require("electron");
const path = require("path");

function createWindow() {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, "preload.js"),
    },
  });

  win.loadFile("index.html");
}

app.whenReady().then(() => {
  createWindow();

  app.on("activate", () => {
    if (BrowserWindow.getAllWindows().length === 0) {
      createWindow();
    }
  });
});

app.on("window-all-closed", () => {
  if (process.platform !== "darwin") {
    app.quit();
  }
});
```

```js
// preload.js

window.addEventListener("DOMContentLoaded", () => {
  const replaceText = (selector, text) => {
    const element = document.getElementById(selector);
    if (element) element.innerText = text;
  };

  for (const type of ["chrome", "node", "electron"]) {
    replaceText(`${type}-version`, process.versions[type]);
  }
});
```

```html
<!-- index.html -->

<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello World!</title>
    <meta
      http-equiv="Content-Security-Policy"
      content="script-src 'self' 'unsafe-inline';"
    />
  </head>
  <body>
    <h1>Hello World!</h1>
    <p>
      We are using Node.js <span id="node-version"></span>, Chromium
      <span id="chrome-version"></span>, and Electron
      <span id="electron-version"></span>.
    </p>
  </body>
</html>
```

package.json의 실행 script도 추가해준다.

```json
{
  "scripts": {
    "start": "electron ."
  }
}
```

잘 나오는 것을 볼 수 있다.
![result](./img/introduction_01.png)

---

electron 파일을 배포하기 위해서는 electron-forge를 설치해야 한다. 다음과 같은 커멘드로 현재 운영체제에 맞는 프로그램을 생성할 수 있다.

```
npm install --save-dev @electron-forge/cli
npx electron-forge import

npm run make
```

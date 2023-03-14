---
layout: default
title: Using Preload Scripts
nav_order: 2
parent: Electron
---

## Using Preload Scripts

### Preload script란

Electron의 메인 프로세스는 운영체제에 접근 가능한 Node.js환경이다. renderer 프로세스에서는 보안상의 이유로 Node.js를 실행하지 않는다. 따라서 이를 이어주는 preload라는 스크립트가 필요하다.

```js
// preload.js

const { contextBridge } = require("electron");

contextBridge.exposeInMainWorld("versions", {
  node: () => process.versions.node,
  chrome: () => process.versions.chrome,
  electron: () => process.versions.electron,
  // we can also expose variables, not just functions
});
```

다음과 같이 preload.js에서 versions.node, versions.chrome, versions.electron을 노출시켰다.

```js
// main.js

const { app, BrowserWindow } = require("electron");
const path = require("path");

const createWindow = () => {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, "preload.js"),
    },
  });

  win.loadFile("index.html");
};

app.whenReady().then(() => {
  createWindow();
});
```

그 후 main.js에서 BrowserWindow를 만들때 webPreferences에서 preload의 path를 넣어주었다.

```js
// renderer.js

const information = document.getElementById("info");
information.innerText = `This app is using Chrome (v${versions.chrome()}), Node.js (v${versions.node()}), and Electron (v${versions.electron()})`;
```

그러면 renderer.js에서 노출시켰던 versions를 사용할 수 있게 된다.

---

Electron의 메인 프로세스와 Renderer 프로세스는 서로 다른 역할을 하며 상호 교환할 수 없다. 즉, Renderer 프로세스에서 직접 Node.js API에 액세스하거나 main 프로세스에서 HTML DOM에 직접 액세스할 수 없다.

이를 해결하기 위해 ipcMain모듈을 사용한다. 웹페이지에서 main 프로세스에 메시지를 보내려면, main에서는 ipcMain.handle을 통해 setup하고 preload에서는 ipcMain.invoke를 통해 노출시키면 된다.

```js
// preload.js

const { contextBridge, ipcRenderer } = require("electron");

contextBridge.exposeInMainWorld("versions", {
  node: () => process.versions.node,
  chrome: () => process.versions.chrome,
  electron: () => process.versions.electron,
  ping: () => ipcRenderer.invoke("ping"),
  // we can also expose variables, not just functions
});
```

```js
// main.js

const { app, BrowserWindow, ipcMain } = require("electron");
const path = require("path");

const createWindow = () => {
  const win = new BrowserWindow({
    width: 800,
    height: 600,
    webPreferences: {
      preload: path.join(__dirname, "preload.js"),
    },
  });
  ipcMain.handle("ping", () => "pong");
  win.loadFile("index.html");
};
app.whenReady().then(createWindow);
```

```js
// renderer.js

const func = async () => {
  const response = await window.versions.ping();
  console.log(response); // prints out 'pong'
};

func();
```

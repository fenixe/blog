---
title: electron
date: 2020-09-17 17:19:29
caregories:
- Hybrid
tags:
- Electron
---

# Base
构建跨平台 桌面应用 框架

# MacOS
## 问题
### 复制功能
main.js
``` js
if (serve) {
  win.webContents.openDevTools();
}

// globaShortcut wil be rewrote by another electron app, just use menu accelerator for each app
globalShortcut.register("Ctrl+Shift+I", () => {
  win.webContents.openDevTools();
});

// MacOS
if (process.platform === "darwin") {
  const template = [
    {
      label: "Application",
      submenu: [
        { label: "Quit", accelerator: "Command+Q", click: () => app.quit()}
      ]
    },
    {
      label: "Edit",
      submenu: [
        { label: "Copy", accelerator: "CmdOrCtrl+C", selector: "copy:" },
        { label: "Paste", accelerator: "CmdOrCtrl+V", selector: "paste:" },
        { label: "Select All", accelerator: "CmdOrCtrl+A", selector: "selectAll:" }
      ]
    }
  ];
  Menu.setApplicationMenu(Menu.buildFromTemplate(template));
} else {
  Menu.setApplicationMenu(null);
}
```

### electron 安装失败
``` zsh
> electron@8.2.1 postinstall /usr/local/lib/node_modules/electron
> node install.js

(node:6406) UnhandledPromiseRejectionWarning: HTTPError: Response code 404 (Not Found) for http://npmmirror.com/mirrors/electron/9.1.0/electron-v8.2.1-darwin-x64.zip

HTTPError: Response code 404 (Not Found) for http://npmmirror.com/mirrors/electron/8.2.1/electron-v9.1.0-darwin-x64.zip
```

解决：
I solved the problem, if you're using taobao mirror, you should config like this in your `~/.npmrc` file:
```
electron_mirror=https://npmmirror.com/mirrors/electron/
electron_custom_dir=7.0.0
```

  1 electron_mirror=http://npmmirror.com/mirrors/electron/
  2 electron_custom_dir=8.2.1
  3 //registry.npmjs.org/:_authToken=d1af3386-c8b9-433d-bd19-a1533fe4f0bd

2024-04-14更新：
设置 阿里镜像无法安装，
最后设置electron_mirror成功
npm config set electron_mirror https://npmmirror.com/mirrors/electron/

#### Electron failed to install correctly, please delete node_modules/electron and try installing again
node_modules/@electron/get/dist/cjs/artifact-utils.js
``` js
// const BASE_URL = 'https://github.com/electron/electron/releases/download/';
const BASE_URL = 'http://npmmirror.com/mirrors/electron/';
```
node ./node_modules/electron/install.js

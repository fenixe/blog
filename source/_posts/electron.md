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

## 版本选择
Electron 发行时间表
https://www.electronjs.org/zh/docs/latest/tutorial/electron-timelines

选择了26版本，此大版本不在更新，2024年2月20日终止。
v26.6.10

使用
"electron": "27.1.0"

## 基础客户端
package.json
```json
"devDependencies": {
    "electron": "27.1.0"
},
```
preload.js
```js
window.addEventListener('DOMContentLoaded', () => {
  const replaceText = (selector, text) => {
    const element = document.getElementById(selector)
    if (element) element.innerText = text
  }

  for (const dependency of ['chrome', 'node', 'electron']) {
    replaceText(`${dependency}-version`, process.versions[dependency])
  }
})
```
main.js
```js
const { app, BrowserWindow } = require('electron')
const path = require('node:path')

const createWindow = () => {
  const win = new BrowserWindow({
    width: 1740,
    height: 1140,
    webPreferences: {
      preload: path.join(__dirname, 'preload.js')
    }
  })

  const ses = win.webContents.session;
  ses.setPermissionRequestHandler((webContents, permission, callback) => {
    const url = webContents.getURL();

    if (permission === 'script-src' && !url.startsWith('file://')) {
      // 允许加载外部脚本
      return callback("script-src 'self' 'unsafe-inline'");
    }

    // 其他情况使用默认策略
    return callback(null);
  });

  win.loadFile('./dist/index.html')
}

app.whenReady().then(() => {
  createWindow()

  app.on('activate', () => {
    if (BrowserWindow.getAllWindows().length === 0) createWindow()
  })
})

app.on('window-all-closed', () => {
  if (process.platform !== 'darwin') app.quit()
})
```
tool ui
```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8">
    <!-- https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CSP -->
    <!-- 删除后可引用外部js，但会弱化应用的安全性 -->
    <!-- <meta http-equiv="Content-Security-Policy" content="default-src 'self'; script-src 'self'"> -->
    <title>坐标拾取工具</title>
    <script src="./assets/vue.js"></script>
    <link rel="stylesheet" href="./assets/element.css"/>
    <script src="./assets/element.js"></script>
    <link rel="stylesheet" href="./assets/custom.css">
    <!-- <script src="https://unpkg.com/@element-plus/icons-vue@2.1.0/dist/index.iife.min.js"></script> -->
    <script src="./assets/element-icons-vue.js"></script>

    <script src="./assets/axios.js"></script>
  </head>
  <body>
    <div id="app">
      <div class="container">
        <div class="tools-wrap">
          <div class="tools">
            
            <el-tooltip content="手动标记" placement="bottom" effect="light">
                <el-button class="tool">
                  <el-icon :size="30" :color="'#888888'">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 1024 1024" data-v-ea893728=""><path fill="currentColor" d="M511.552 128c-35.584 0-64.384 28.8-64.384 64.448v516.48L274.048 570.88a94.272 94.272 0 0 0-112.896-3.456 44.416 44.416 0 0 0-8.96 62.208L332.8 870.4A64 64 0 0 0 384 896h512V575.232a64 64 0 0 0-45.632-61.312l-205.952-61.76A96 96 0 0 1 576 360.192V192.448C576 156.8 547.2 128 511.552 128M359.04 556.8l24.128 19.2V192.448a128.448 128.448 0 1 1 256.832 0v167.744a32 32 0 0 0 22.784 30.656l206.016 61.76A128 128 0 0 1 960 575.232V896a64 64 0 0 1-64 64H384a128 128 0 0 1-102.4-51.2L101.056 668.032A108.416 108.416 0 0 1 128 512.512a158.272 158.272 0 0 1 185.984 8.32z"></path></svg>
                  </el-icon>
                </el-button>
            </el-tooltip>
          </div>
          <div class="account">
            <el-avatar :size="45" :src="circleUrl" />
          </div>
        </div>
        <div class="plant-wrap">
          <div class="box">
            <div class="wrap">
                <el-table :data="datas" border stripe style="width: 100%">
                    <el-table-column prop="id" label="ID" width="100"></el-table-column>
                    <el-table-column label="操作" width="128" align="center">
                        <template #default="scope">
                            <el-button type="text" size="small" @click="handleDialog(scope.row)">查看</el-button>
                        </template>
                    </el-table-column>
                </el-table>
                <el-pagination
                    :currentPage="currentPage"
                    :page-size="pageSize"
                    background
                    layout="total, prev, pager, next, jumper"
                    :total="total"
                    @current-change="handleCurrentChange"
                />
            </div>
            <el-dialog
                v-model="dialogVisible"
                title="门店详情"
                width="80%"
                :before-close="handleClose"
            >
            </el-dialog>
          </div>
        </div>
      </div>
     
    </div>
    <script>
        const App = {
            data() {
                return {
                    // serviceAddress: 'http://192.168.9.6:8080',
                    serviceAddress: 'http://127.0.0.1:8080',
                    circleUrl: 'https://cube.elemecdn.com/3/7c/3ea6beec64369c2642b92c6726f1epng.png',
                    list: []
                };
            }
        };
        const app = Vue.createApp(App);
        app.use(ElementPlus);
        app.mount("#app");
    </script>
  </body>
</html>
```

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

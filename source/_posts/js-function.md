---
title: js-function
date: 2020-12-14 10:16:08
categories:
- JavaScript
tags:
- js-function
---

# function
## 排序
数字最大在前
item.options.sort((a, b) => b.num - a.num);
不改变数组，可以使用toSorted()。
## 复制到粘贴板
``` js
copy() {
  const input = document.createElement('input');
  document.body.appendChild(input);
  input.setAttribute('value', this.avatar._id);
  input.select();
  if (document.execCommand('copy')) {
    document.execCommand("copy");
    this.toastService.success("成功复制SN到粘贴板！");
  }
  document.body.removeChild(input);
}
```

### 新方法
```js
async onCopy(){
    try {
        await navigator.clipboard.writeText('hello world');
        console.log('Content copied to clipboard');
        ElMessage({
            message: "复制成功",
            type: "success",
            duration: 2000
        })
    } catch (err) {
        console.error('Failed to copy: ', err);
        ElMessage({
            message: "复制失败，请手动复制链接",
            type: "error",
            duration: 2000
        })
    }
}
```

## 下载图片资源
``` js
import * as JSZip from "jszip";
import * as FileSaver from "file-saver";
async getUrlBase64(urlRemote, ext) {
    return new Promise((resolve, reject) => {
        let canvas = document.createElement("canvas");
        let ctx = canvas.getContext("2d"); // 方法返回canvas 的上下文
        let img = new Image();
        img.crossOrigin = "Anonymous"; // 跨域
        img.src = urlRemote;
        img.onload = () => {
            canvas.width = img.width;
            canvas.height = img.height;
            ctx.drawImage(img, 0, 0); // 在Canvas上绘制图像。
            let dataURL = canvas.toDataURL("image/" + ext); // 返回一个包含图片展示的 data URI 。
            resolve(dataURL);
            canvas = null;
        };
    });
  }
  async exportZip(urls) {
      const imgList = urls;
      const proList = [];
      const zip = new JSZip();
      const cache = {};
      await imgList.forEach(item => { // 等待所有图片转换完成
          const pro = this.getUrlBase64(item, ".png").then((base64: any) => {
              const fileName = item.replace(/(.*\/)*([^.]+)/i, "$2");
              zip.file(fileName, base64.substring(base64.indexOf(",") + 1), {
                  base64: true
              });
              cache[fileName] = base64;
          });
          proList.push(pro);
      });
      Promise.all(proList).then(res => {
          zip.generateAsync({
              type: "blob"
          }).then(content => { // 生成二进制流
            FileSaver(content, `${this.avatar._id}.zip`); // 利用file-saver保存文件
            this.toastService.success("资源下载成功");
          });
      });
  }
```

### url to blob
safari 会出现跨域问题
``` js
// const imgDom = await this.URLtoImage(activeCover.url).catch(() => {});
// if (!imgDom) return this.loadingStatus = false;
// coverImgFile = await this.imageDomToFile(imgDom).catch(() => {});
URLtoImage(url) {
    return new Promise((resolve, reject) => {
        let img = new Image();
        img.crossOrigin = "Anonymous"; // 跨域
        img.src = url;
        img.onload = () => {
            resolve(img);
        };
        img.onerror = () => {
            this.$message.error("图片加载失败");
            reject();
        };
    });
},
imageDomToFile(imgDom) {
    return new Promise((resolve, reject) => {
        let canvas = document.createElement("canvas");
        let ctx = canvas.getContext("2d");
        canvas.width = imgDom.width;
        canvas.height = imgDom.height;
        ctx.drawImage(imgDom, 0, 0);

        canvas.toBlob((blob) => {
            console.log("blob", blob);
            if (!blob) {
                this.$message.error("图片处理失败");
                return reject();
            }

            const imgFile = new File([blob], "image.png", {
                type: "image/png",
            });
            console.log("imgFile", imgFile);
            resolve(imgFile);
        }, "image/png");
    });
},
```

## localDB
``` ts
export const localStore = {
  set: (key: string, obj: object) => {
    localStorage.setItem(key, JSON.stringify(obj));
  },

  get<T>(key: string): T {
    const item = localStorage.getItem(key);

    if (!item) {
      return;
    }

    return JSON.parse(item);
  },

  remove: (key: string) => {
    localStorage.removeItem(key);
  }
};
```

## @input 节流
``` js
  clearTimeout(this.throttleTimer);
  this.throttleTimer = setTimeout(this.busIdDetail, 2000);
```

## Number 转数组
```js
let num1 = 123;
var num2 = num1.toString().split("").map(_ => +_);
num2 //[1,2,3]
// 调用 split 方法后是一个数组，里面的元素是字符串，字符串要转回数字。
// 把_当作是一个遍历后的val,然后再给个加就变成了数字了
```

## 保存py文件
```js
saveScript() {
  // 生成动态的 Python 脚本代码
  const pythonCode = `
    # 这是一个动态生成的 Python 脚本
    print('Hello, World!')
  `;

  // 将脚本代码转换为 Blob 对象
  const blob = new Blob([pythonCode], { type: 'text/plain' });

  // 创建 URL 对象以下载文件
  const url = URL.createObjectURL(blob);

  // 创建链接并模拟点击以下载文件
  const link = document.createElement('a');
  link.download = 'my_script.py';
  link.href = url;
  link.click();

  // 释放 URL 对象
  URL.revokeObjectURL(url);
}
```

## 0对于A，1对应B ，2对于C 依此类推
```js
function numberToLetter(number) {
  // 将数字转换为字母
  var letter = String.fromCharCode(number + 65);
  return letter;
}
```

## 视频
### 视频大小
```js
// input file 转 M
const fileSize = file.size / (1024 * 1024);
```

### 视频时长
```js
let file = e.file;
const video = document.createElement('video');
video.src = URL.createObjectURL(file);
video.addEventListener('loadedmetadata', ()=>{
    console.log('视频长度：', video.duration + ' 秒');
});
```

### 下载PDF
```js
// a4纸的尺寸（595.28,841.89）
```


# 其他
## echarts
双向柱形图
https://www.makeapie.cn/echarts_content/x8YeVj-sL7.html

范围
`>（gt）、>=（gte）、<（lt）、<=（lte）、=（eq）、!=（ne、<>）、reg`

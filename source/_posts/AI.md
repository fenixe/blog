---
title: AI
date: 2024-06-26 18:18:35
categories:
- AI
tags:
- AI
---

# Base



# Code
## 流式输出
``` js
const response = await fetch('/chatapi/chat-process', {
  method: "POST",
  body: param
});

if (!response.body) return;
const reader = response.body.pipeThrough(new TextDecoderStream()).getReader();

const decoder = new TextDecoder();
let result = '';
while (true) {
  var { value, done } = await reader.read();
  console.log("KF done status:", done);
  if (done) break;
  
  // Split the received chunk by newline and try parsing each line as JSON
  const lines = value.split('\n');
  lines.forEach(line => {
    if (line) {
      try {
        const parsedLine = JSON.parse(line);
        if (parsedLine && parsedLine.text) {
          this.content += parsedLine.text; // Update the component's content data
        }
      } catch (error) {
        console.error("Error parsing JSON line:", error, line);
      }
    }
  });
}
```



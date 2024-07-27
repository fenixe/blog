---
title: AI
date: 2024-06-26 18:18:35
categories:
- AI
tags:
- AI
---

# Base
## Top-p
Top-p（也称为核采样）是一种用于控制生成模型输出的技术。它通过选择概率质量总和达到某个阈值的最小集合中的词来限制生成的词汇表。这个阈值由`p`参数控制。设置`p`的最佳值取决于具体的应用场景和生成质量的要求。以下是一些指导原则，可以帮助你找到适合的`p`值：

1. **理解Top-p的作用**：
   - **Top-p = 1.0**：相当于没有限制，模型可以选择所有可能的词。
   - **Top-p < 1.0**：限制模型只选择概率质量总和达到`p`的词，这通常会减少生成的多样性，但可能提高生成的连贯性和质量。

2. **常见的Top-p值**：
   - **0.9**：这是一个常见的默认值，通常能在生成质量和多样性之间取得良好的平衡。
   - **0.8**：进一步减少多样性，可能会提高生成的连贯性，适用于需要更严格控制输出的场景。
   - **0.95**：增加多样性，适用于需要更多创意或探索性输出的场景。

3. **实验和调整**：
   - **具体应用场景**：不同的应用场景对生成内容的要求不同。对于对话生成、故事创作等需要更多创意的任务，可以尝试较高的`p`值（如0.9或0.95）。对于技术文档生成、代码补全等需要更高准确性的任务，可以尝试较低的`p`值（如0.8或0.85）。
   - **逐步调整**：从一个常见的默认值（如0.9）开始，根据生成结果逐步调整`p`值。观察生成内容的连贯性、多样性和质量，找到最适合的设置。

4. **结合其他参数**：
   - **温度（Temperature）**：温度参数控制生成的随机性。可以结合调整温度参数（通常在0.7到1.0之间）和Top-p值，找到最佳的生成效果。

5. **自动化调参**：
   - 如果有大量的生成任务，可以考虑使用自动化调参方法（如网格搜索或贝叶斯优化）来找到最佳的`p`值和其他参数组合。

总之，Top-p的最佳设置需要根据具体的应用场景和生成要求进行实验和调整。通过逐步调整和观察生成结果，你可以找到最适合的`p`值。


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



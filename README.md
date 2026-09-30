# Office 文件在线预览

## 两种使用模式

### 1. Demo 模式

直接访问页面，不带参数时进入 Demo 模式，可以点击按钮或输入 URL 切换预览：

```
https://bird-quezai.github.io/office-prwview/
```

### 2. 纯预览模式

在地址栏后加 `?file=` 或 `?url=` 参数，直接渲染预览内容（参数值需 `encodeURIComponent` 编码）：

```
# 基础用法
?file=https%3A%2F%2Fexample.com%2Ffiles%2Freport.pdf

# 带鉴权 token 的文件
?file=https%3A%2F%2Fexample.com%2Ffiles%2Freport.pdf%3Ftoken%3Dabc123
```

#### 其他页面跳转预览

```js
const fileUrl = 'https://example.com/files/report.pdf?token=abc123';
const previewUrl = `${window.location.origin}/office-prwview/?file=${encodeURIComponent(fileUrl)}`;
window.open(previewUrl, '_blank');
```

## 嵌入到其他 Vue 项目

```vue
<script setup>
import { ref } from 'vue';
import FilePreview from './components/FilePreview.vue';

const docContent = ref('https://example.com/files/report.pdf');
</script>

<template>
  <div style="height: 100vh">
    <FilePreview :docContent="docContent" />
  </div>
</template>
```

## 支持的文件格式

PDF（.pdf）、Word（.doc / .docx）、Excel（.xls / .xlsx）、PPT（.ppt / .pptx）
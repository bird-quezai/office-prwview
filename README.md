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

# 指定解析类型（优先于文件后缀名，可选值：doc/docx/xls/xlsx/ppt/pptx/pdf）
?file=https%3A%2F%2Fexample.com%2Fdownload%3Fid%3D123&type=pdf
```

`type` 参数仅接受上述限定类型（大小写不敏感，可带前导点如 `.pdf`）；传入非法类型时自动回退到文件后缀名解析。

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

如需在文件地址无后缀或后缀不准确时指定解析类型，可额外传入 `docType`（可选值同上，非法值自动回退后缀名）：

```vue
<FilePreview :docContent="docContent" docType="pdf" />
```

## 构建与发布

项目提供 Makefile，统一使用 pnpm 作为包管理器：

| 命令 | 说明 |
| --- | --- |
| `make install` | 安装依赖 |
| `make dev` | 启动本地开发服务 |
| `make build` | 构建生产包到 `dist/` |
| `make preview` | 构建后本地预览产物 |
| `make deploy` | 构建并发布到 GitHub Pages |
| `make clean` | 清理 `dist/` |

发布命令与 package.json 的 `gh-deploy` 一致：

```
pnpm exec gh-pages -d dist -r https://github.com/bird-quezai/office-prwview.git
```

## 支持的文件格式

PDF（.pdf）、Word（.doc / .docx）、Excel（.xls / .xlsx）、PPT（.ppt / .pptx）
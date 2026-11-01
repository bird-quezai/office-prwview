# Office 文件在线预览 · Markdown 示例

这是一个用于演示 **Markdown 渲染** 的示例文档，支持常见语法。

## 支持的能力

- 标题、段落与**加粗**、*斜体*
- 有序 / 无序列表
- 代码块与行内代码
- 表格
- 引用与分割线

## 代码示例

```js
import { marked } from 'marked';

const html = marked.parse('# Hello Markdown');
console.log(html);
```

## 表格示例

| 格式 | 说明 |
| --- | --- |
| TXT | 纯文本，保留换行 |
| Markdown | 渲染为富文本展示 |

## 引用

> 预览内容来自外部文件，渲染前已做安全过滤，避免脚本注入。

---

更多用法请查看项目 README。

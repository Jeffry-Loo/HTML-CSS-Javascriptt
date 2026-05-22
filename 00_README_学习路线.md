# HTML / CSS / JavaScript 完整学习路线

> 目标：从零开始看懂网页如何组成，并能独立写出一个结构清楚、样式稳定、交互可靠的小型网页应用。

## 这套资料怎么学

学习 Web 前端最容易混乱的地方，是把 HTML、CSS、JavaScript 当成三门互不相干的语言。其实它们是同一个网页的三层：

1. HTML 负责内容和结构：页面上有什么。
2. CSS 负责样式和布局：这些内容长什么样、放在哪里。
3. JavaScript 负责行为和数据：用户点击、输入、请求数据时发生什么。

建议学习顺序：

1. 先学 HTML，能写出语义正确的页面骨架。
2. 再学 CSS，能把页面排版成稳定、响应式的界面。
3. 再学 JavaScript，能读写页面、处理事件、保存和请求数据。
4. 最后做综合项目，把三者连接起来。

## 章节目录

- [01_HTML_结构与语义.md](01_HTML_结构与语义.md)
- [02_CSS_选择器盒模型布局响应式.md](02_CSS_选择器盒模型布局响应式.md)
- [03_JavaScript_语言基础.md](03_JavaScript_语言基础.md)
- [04_DOM_事件_异步_浏览器API.md](04_DOM_事件_异步_浏览器API.md)
- [05_综合项目_任务看板.md](05_综合项目_任务看板.md)
- [06_速查表_练习题_学习检查清单.md](06_速查表_练习题_学习检查清单.md)

示例项目：

- [examples/task-board/index.html](examples/task-board/index.html)

## 核心心法

写网页时，永远先问三个问题：

1. 这是什么内容？用 HTML 表达。
2. 它应该如何呈现？用 CSS 表达。
3. 用户能对它做什么？用 JavaScript 表达。

例如一个“添加任务”的功能：

```html
<form id="taskForm">
  <label for="taskInput">任务名称</label>
  <input id="taskInput" name="title" required>
  <button type="submit">添加</button>
</form>
```

HTML 说明这里有一个表单、一个输入框、一个按钮。CSS 决定它们的大小、颜色、间距。JavaScript 监听提交事件，把输入值变成任务卡片。

## 官方参考资料

这些资料用于校对本笔记的技术点，优先级高于博客和短视频：

- MDN HTML 入门与参考：https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Structuring_content
- MDN HTML 元素参考：https://developer.mozilla.org/en-US/docs/Web/HTML/Reference/Elements
- WHATWG HTML Living Standard：https://html.spec.whatwg.org/
- MDN CSS 入门与参考：https://developer.mozilla.org/en-US/docs/Learn_web_development/Core/Styling_basics
- MDN CSS Reference：https://developer.mozilla.org/en-US/docs/Web/CSS/Reference
- MDN JavaScript Guide：https://developer.mozilla.org/en-US/docs/Web/JavaScript/Guide
- MDN DOM Introduction：https://developer.mozilla.org/en-US/docs/Web/API/Document_Object_Model/Introduction
- MDN Fetch API：https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API
- ECMAScript Language Specification：https://tc39.es/ecma262/


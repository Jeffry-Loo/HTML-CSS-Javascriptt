# 第 1 章：HTML 结构与语义

HTML 是 HyperText Markup Language，意思是“超文本标记语言”。它不是编程语言，而是用标签描述内容结构的语言。

HTML 的重点不是“让页面变好看”，而是准确告诉浏览器和辅助技术：这里是什么内容。

## 1.1 一个完整 HTML 文件

```html
<!doctype html>
<html lang="zh-CN">
  <head>
    <meta charset="utf-8">
    <meta name="viewport" content="width=device-width, initial-scale=1">
    <title>我的网页</title>
    <link rel="stylesheet" href="styles.css">
  </head>
  <body>
    <header>
      <h1>我的网页</h1>
    </header>

    <main>
      <p>这是页面的主要内容。</p>
    </main>

    <script src="app.js"></script>
  </body>
</html>
```

逐行理解：

- `<!doctype html>`：告诉浏览器使用现代 HTML 标准解析页面。
- `<html lang="zh-CN">`：根元素，`lang` 告诉浏览器页面主要语言。
- `<head>`：放页面元信息，不直接显示在页面主体里。
- `<meta charset="utf-8">`：声明字符编码，避免中文乱码。
- `<meta name="viewport"...>`：让页面在手机上按设备宽度显示。
- `<title>`：浏览器标签页标题，也会影响搜索结果标题。
- `<link rel="stylesheet">`：连接 CSS 文件。
- `<body>`：用户能看到和操作的页面主体。
- `<script src="app.js">`：连接 JavaScript 文件。

## 1.2 标签、元素、属性

```html
<a href="https://developer.mozilla.org/" target="_blank">打开 MDN</a>
```

- `<a>` 是开始标签。
- `</a>` 是结束标签。
- 整段是一个元素。
- `href` 和 `target` 是属性。
- `打开 MDN` 是元素内容。

有些元素没有结束标签，例如：

```html
<img src="photo.jpg" alt="一张产品照片">
<input type="email" name="email">
<br>
```

## 1.3 标题和段落

标题从 `h1` 到 `h6`，表示内容层级：

```html
<h1>前端学习笔记</h1>
<h2>HTML</h2>
<h3>表单</h3>
```

原则：

- 一个页面通常只有一个主要 `h1`。
- 不要为了字体大小乱用标题级别。
- 标题级别应该像目录一样逐层展开。

段落用 `p`：

```html
<p>HTML 用来描述页面内容的结构。</p>
```

换行不要滥用 `br`。如果是两个自然段，应该写两个 `p`。

## 1.4 文本语义

HTML 有很多标签能表达文字含义：

```html
<p><strong>重要：</strong>提交前请检查邮箱。</p>
<p><em>建议</em>每天练习 30 分钟。</p>
<p>快捷键是 <kbd>Ctrl</kbd> + <kbd>S</kbd>。</p>
<p>变量名可以写成 <code>taskList</code>。</p>
```

常用文本语义：

- `strong`：重要内容。
- `em`：强调内容。
- `code`：代码片段。
- `kbd`：键盘输入。
- `mark`：标记高亮。
- `small`：附属说明。

不要只为了粗体使用 `strong`。如果只是视觉样式，交给 CSS。

## 1.5 链接

链接使用 `a`：

```html
<a href="about.html">关于我们</a>
<a href="https://example.com">外部网站</a>
<a href="#contact">跳到联系方式</a>
<a href="mailto:hello@example.com">发送邮件</a>
```

好链接文本应该能独立表达目的：

```html
<!-- 不好 -->
<a href="report.pdf">点击这里</a>

<!-- 更好 -->
<a href="report.pdf">下载课程报告 PDF</a>
```

如果用 `target="_blank"` 打开新页面，建议加：

```html
<a href="https://example.com" target="_blank" rel="noopener noreferrer">外部网站</a>
```

## 1.6 图片与替代文本

```html
<img src="profile.jpg" alt="Jeffry 的头像">
```

`alt` 很重要：

- 图片加载失败时显示。
- 屏幕阅读器会读出来。
- 搜索引擎会参考它理解图片。

写 `alt` 的方法：

- 如果图片传达信息，描述信息。
- 如果图片只是装饰，可以写空值 `alt=""`。
- 不要写“图片”“照片”，因为 `img` 已经说明它是图片。

例子：

```html
<!-- 信息型图片 -->
<img src="chart.png" alt="2026 年 1 月到 5 月销售额逐月上升">

<!-- 装饰型图片 -->
<img src="divider.png" alt="">
```

## 1.7 列表

无序列表：

```html
<ul>
  <li>HTML</li>
  <li>CSS</li>
  <li>JavaScript</li>
</ul>
```

有序列表：

```html
<ol>
  <li>创建 HTML</li>
  <li>编写 CSS</li>
  <li>添加 JavaScript</li>
</ol>
```

描述列表：

```html
<dl>
  <dt>HTML</dt>
  <dd>描述页面结构。</dd>
  <dt>CSS</dt>
  <dd>描述页面样式。</dd>
</dl>
```

## 1.8 页面结构语义

现代 HTML 推荐使用语义化结构：

```html
<body>
  <header>
    <h1>任务管理器</h1>
    <nav>
      <a href="/">首页</a>
      <a href="/tasks">任务</a>
    </nav>
  </header>

  <main>
    <section>
      <h2>今日任务</h2>
      <article>
        <h3>完成 HTML 笔记</h3>
        <p>整理结构标签和表单知识。</p>
      </article>
    </section>
  </main>

  <aside>
    <h2>提示</h2>
    <p>先写结构，再写样式。</p>
  </aside>

  <footer>
    <small>&copy; 2026 Jeffry</small>
  </footer>
</body>
```

常见结构标签：

- `header`：页头或区域头部。
- `nav`：主要导航。
- `main`：页面唯一主要内容。
- `section`：有主题的一组内容，通常需要标题。
- `article`：独立可分发内容，如文章、卡片、评论。
- `aside`：补充内容。
- `footer`：页脚或区域底部。

## 1.9 表格

表格用于展示二维数据，不要用表格做页面布局。

```html
<table>
  <caption>课程进度</caption>
  <thead>
    <tr>
      <th scope="col">章节</th>
      <th scope="col">主题</th>
      <th scope="col">状态</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>1</td>
      <td>HTML 结构</td>
      <td>完成</td>
    </tr>
  </tbody>
</table>
```

关键点：

- `caption` 描述表格内容。
- `thead`、`tbody`、`tfoot` 分组。
- `th` 是表头单元格。
- `scope` 帮助辅助技术理解表头对应方向。

## 1.10 表单

表单是网页收集用户输入的核心。

```html
<form action="/signup" method="post">
  <label for="email">邮箱</label>
  <input id="email" name="email" type="email" required>

  <label for="password">密码</label>
  <input id="password" name="password" type="password" minlength="8" required>

  <button type="submit">注册</button>
</form>
```

表单重点：

- 每个输入控件尽量配 `label`。
- `for` 要对应输入框的 `id`。
- `name` 是提交数据时的字段名。
- `type` 决定输入规则和手机键盘类型。
- `required`、`minlength`、`pattern` 等可做基础验证。

常见输入类型：

```html
<input type="text">
<input type="email">
<input type="password">
<input type="number">
<input type="date">
<input type="checkbox">
<input type="radio">
<input type="file">
```

下拉、长文本：

```html
<label for="level">难度</label>
<select id="level" name="level">
  <option value="beginner">入门</option>
  <option value="advanced">进阶</option>
</select>

<label for="note">备注</label>
<textarea id="note" name="note" rows="4"></textarea>
```

## 1.11 按钮类型

```html
<button type="button">普通按钮</button>
<button type="submit">提交表单</button>
<button type="reset">重置表单</button>
```

在表单内部，如果 `button` 没写 `type`，默认通常是提交。为了避免意外提交，建议明确写 `type`。

## 1.12 HTML 与 CSS、JavaScript 的连接

连接 CSS：

```html
<link rel="stylesheet" href="styles.css">
```

连接 JavaScript：

```html
<script src="app.js" defer></script>
```

`defer` 的作用：脚本会在 HTML 解析完成后执行，适合大多数页面脚本。

HTML 可以通过 `class` 给 CSS 找元素：

```html
<article class="task-card">...</article>
```

JavaScript 可以通过 `id` 或选择器找元素：

```html
<form id="taskForm">...</form>
```

```js
const form = document.querySelector("#taskForm");
```

## 1.13 可访问性基础

可访问性不是额外功能，而是好 HTML 的自然结果。

基本规则：

- 图片写合理 `alt`。
- 表单控件关联 `label`。
- 按钮用 `button`，链接用 `a`。
- 页面标题层级清晰。
- 不要只靠颜色传达信息。
- 交互元素要能用键盘操作。

错误示例：

```html
<div onclick="save()">保存</div>
```

更好：

```html
<button type="button" onclick="save()">保存</button>
```

## 1.14 常见错误

错误 1：标签没有正确嵌套。

```html
<!-- 错 -->
<p><strong>重要</p></strong>

<!-- 对 -->
<p><strong>重要</strong></p>
```

错误 2：重复使用同一个 `id`。

```html
<!-- 错：同一页面 id 应唯一 -->
<input id="email">
<input id="email">
```

错误 3：用 `div` 写所有东西。

```html
<!-- 不够语义化 -->
<div class="title">文章标题</div>

<!-- 更好 -->
<h1>文章标题</h1>
```

## 1.15 本章练习

练习 1：写一个个人介绍页，包含：

- 页面标题。
- 头像。
- 三个兴趣爱好列表。
- 一个联系方式表单。
- 页头、主体、页脚。

练习 2：把下面这段内容改成语义化 HTML：

```text
我的课程
HTML：学习网页结构
CSS：学习网页样式
JavaScript：学习网页交互
```

参考答案：

```html
<section>
  <h2>我的课程</h2>
  <dl>
    <dt>HTML</dt>
    <dd>学习网页结构</dd>
    <dt>CSS</dt>
    <dd>学习网页样式</dd>
    <dt>JavaScript</dt>
    <dd>学习网页交互</dd>
  </dl>
</section>
```


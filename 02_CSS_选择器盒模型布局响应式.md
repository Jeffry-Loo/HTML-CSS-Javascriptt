# 第 2 章：CSS 选择器、盒模型、布局与响应式

CSS 是 Cascading Style Sheets，意思是“层叠样式表”。它负责控制页面的视觉呈现：颜色、字体、间距、边框、布局、动画、响应式效果。

CSS 的核心问题是：选中哪些元素，并给它们应用什么样式。

## 2.1 引入 CSS 的三种方式

推荐方式：外部样式表。

```html
<link rel="stylesheet" href="styles.css">
```

```css
body {
  font-family: Arial, sans-serif;
}
```

另外两种方式：

```html
<style>
  p {
    color: blue;
  }
</style>
```

```html
<p style="color: blue;">这是一段文字。</p>
```

实际项目中，优先使用外部 CSS 文件。内联样式难维护，除非是很特殊的动态样式。

## 2.2 CSS 规则结构

```css
.card {
  color: #222;
  background-color: white;
  padding: 16px;
}
```

- `.card` 是选择器。
- `{ ... }` 内是声明块。
- `color: #222;` 是一条声明。
- `color` 是属性。
- `#222` 是值。

## 2.3 常用选择器

```css
/* 元素选择器 */
p {
  line-height: 1.6;
}

/* 类选择器 */
.task-card {
  border: 1px solid #ddd;
}

/* ID 选择器 */
#mainTitle {
  font-size: 32px;
}

/* 后代选择器 */
.card p {
  color: #555;
}

/* 子元素选择器 */
.menu > li {
  list-style: none;
}

/* 属性选择器 */
input[type="email"] {
  border-color: #2563eb;
}

/* 伪类 */
button:hover {
  background-color: #111827;
}

/* 伪元素 */
p::first-line {
  font-weight: bold;
}
```

建议：

- 页面上可复用的样式用 `class`。
- 少用 `id` 写 CSS，因为优先级太高。
- 选择器不要写得过长，避免维护困难。

## 2.4 层叠、继承、优先级

CSS 的 C 就是 Cascading，层叠。多个规则作用到同一元素时，浏览器会决定谁生效。

优先级大致顺序：

1. 内联样式：`style="..."`。
2. ID 选择器：`#id`。
3. 类、属性、伪类：`.class`、`[type]`、`:hover`。
4. 元素、伪元素：`p`、`::before`。

如果优先级相同，后写的覆盖先写的。

```css
p {
  color: blue;
}

p {
  color: red;
}
```

最终是红色。

继承：有些属性会从父元素传给子元素，如 `color`、`font-family`。有些不会，如 `margin`、`border`。

## 2.5 盒模型

页面上的每个元素都像一个盒子：

```text
content -> padding -> border -> margin
```

```css
.box {
  width: 200px;
  padding: 16px;
  border: 2px solid #111;
  margin: 20px;
}
```

默认情况下，`width` 只表示内容宽度，不包括 `padding` 和 `border`。实际占用宽度是：

```text
200 + 16*2 + 2*2 = 236px
```

更常用的写法：

```css
* {
  box-sizing: border-box;
}
```

这样 `width` 会包含 `padding` 和 `border`，布局更直观。

## 2.6 Display

```css
.hidden {
  display: none;
}

.inline {
  display: inline;
}

.block {
  display: block;
}

.flex {
  display: flex;
}

.grid {
  display: grid;
}
```

常见区别：

- `block`：独占一行，可设置宽高，如 `div`、`p`。
- `inline`：不独占一行，宽高通常不生效，如 `span`、`a`。
- `inline-block`：像 inline 一样同行，又能设置宽高。
- `flex`：一维布局，适合横向或纵向排列。
- `grid`：二维布局，适合行列同时控制。

## 2.7 Flexbox 一维布局

Flexbox 适合做导航、工具栏、卡片行、居中布局。

```css
.toolbar {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 12px;
}
```

主轴与交叉轴：

- `flex-direction: row` 时，主轴是横向。
- `justify-content` 控制主轴对齐。
- `align-items` 控制交叉轴对齐。

常用属性：

```css
.container {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  gap: 16px;
  justify-content: center;
  align-items: stretch;
}

.item {
  flex: 1 1 240px;
}
```

`flex: 1 1 240px` 可以理解为：

- 可以放大。
- 可以缩小。
- 初始宽度约 240px。

## 2.8 Grid 二维布局

Grid 适合页面大布局、卡片网格、仪表盘。

```css
.cards {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 16px;
}
```

响应式卡片网格：

```css
.cards {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
  gap: 16px;
}
```

这句很实用：

- `auto-fit`：自动放下尽可能多的列。
- `minmax(220px, 1fr)`：每列最小 220px，空间够时平均分。

页面布局例子：

```css
.page {
  display: grid;
  grid-template-columns: 240px 1fr;
  min-height: 100vh;
}
```

## 2.9 Position 定位

```css
.box {
  position: static;
}
```

常见值：

- `static`：默认正常文档流。
- `relative`：相对自己原位置偏移。
- `absolute`：相对最近的非 static 定位祖先定位。
- `fixed`：相对浏览器窗口定位。
- `sticky`：滚动到某位置后粘住。

例子：

```css
.card {
  position: relative;
}

.badge {
  position: absolute;
  top: 8px;
  right: 8px;
}
```

`absolute` 常见坑：如果父元素没有 `position: relative`，它可能跑到别的参照物上。

## 2.10 字体与文本

```css
body {
  font-family: Arial, "Microsoft YaHei", sans-serif;
  font-size: 16px;
  line-height: 1.6;
  color: #1f2937;
}

h1 {
  font-size: 2rem;
  font-weight: 700;
}

p {
  text-align: left;
}
```

常用单位：

- `px`：固定像素。
- `%`：相对父元素。
- `em`：相对当前元素字体大小。
- `rem`：相对根元素字体大小。
- `vw` / `vh`：相对视口宽高。

正文建议用 `rem` 或 `px`，布局宽度常用 `%`、`rem`、`fr`、`minmax()`。

## 2.11 颜色

```css
:root {
  --color-bg: #f8fafc;
  --color-text: #111827;
  --color-primary: #2563eb;
}

body {
  background: var(--color-bg);
  color: var(--color-text);
}

button {
  background: var(--color-primary);
}
```

CSS 自定义属性，也叫 CSS 变量，适合统一主题颜色、间距、阴影。

注意对比度：浅色文字不要放在浅色背景上，深色文字不要放在深色背景上。

## 2.12 响应式设计

响应式设计指页面能适配手机、平板、桌面。

基础设置：

```html
<meta name="viewport" content="width=device-width, initial-scale=1">
```

常见写法：

```css
.layout {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

@media (min-width: 768px) {
  .layout {
    grid-template-columns: 240px 1fr;
  }
}
```

这叫 mobile-first：先写手机样式，再用媒体查询增强大屏布局。

图片响应式：

```css
img {
  max-width: 100%;
  height: auto;
}
```

容器限制：

```css
.container {
  width: min(100% - 32px, 1120px);
  margin-inline: auto;
}
```

## 2.13 状态样式

交互元素要写状态：

```css
button {
  cursor: pointer;
}

button:hover {
  background: #1d4ed8;
}

button:focus-visible {
  outline: 3px solid #93c5fd;
  outline-offset: 2px;
}

button:disabled {
  opacity: 0.5;
  cursor: not-allowed;
}
```

`focus-visible` 对键盘用户特别重要。

## 2.14 过渡与动画

过渡：

```css
.card {
  transition: transform 160ms ease, box-shadow 160ms ease;
}

.card:hover {
  transform: translateY(-2px);
  box-shadow: 0 10px 24px rgba(15, 23, 42, 0.12);
}
```

动画：

```css
@keyframes fade-in {
  from {
    opacity: 0;
    transform: translateY(8px);
  }
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.panel {
  animation: fade-in 240ms ease both;
}
```

不要给所有东西都加动画。动画应该帮助用户理解变化，而不是分散注意力。

## 2.15 CSS 文件组织建议

小项目可以这样组织：

```css
/* 1. 基础变量 */
:root {}

/* 2. 全局重置 */
* {}
body {}

/* 3. 页面布局 */
.app {}
.sidebar {}

/* 4. 组件 */
.button {}
.card {}

/* 5. 工具类 */
.sr-only {}
.hidden {}
```

命名建议：

```css
.task-card {}
.task-card__title {}
.task-card--done {}
```

意思：

- `task-card`：组件。
- `task-card__title`：组件内部元素。
- `task-card--done`：组件状态或变体。

## 2.16 常见错误

错误 1：用固定宽度导致手机溢出。

```css
/* 不好 */
.card {
  width: 900px;
}

/* 更好 */
.card {
  width: min(100%, 900px);
}
```

错误 2：滥用 `!important`。

```css
.title {
  color: red !important;
}
```

`!important` 会让后续维护变难。优先调整选择器和文件顺序。

错误 3：忘记 `box-sizing`。

```css
*,
*::before,
*::after {
  box-sizing: border-box;
}
```

## 2.17 本章练习

练习 1：把三个卡片排成响应式网格：

- 手机一列。
- 平板两列。
- 桌面三列。

参考：

```css
.cards {
  display: grid;
  grid-template-columns: 1fr;
  gap: 16px;
}

@media (min-width: 640px) {
  .cards {
    grid-template-columns: repeat(2, 1fr);
  }
}

@media (min-width: 1024px) {
  .cards {
    grid-template-columns: repeat(3, 1fr);
  }
}
```

练习 2：写一个按钮，包含默认、悬停、聚焦、禁用四种状态。

练习 3：用 Flexbox 写一个顶部导航，左边是 logo，右边是链接。


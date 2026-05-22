# 第 4 章：DOM、事件、异步与浏览器 API

JavaScript 真正在网页里发挥作用，靠的是浏览器提供的 API。最核心的是 DOM。

DOM 是 Document Object Model，文档对象模型。浏览器把 HTML 解析成一棵节点树，JavaScript 可以读取和修改这棵树。

## 4.1 选择元素

HTML：

```html
<h1 id="title">任务列表</h1>
<ul class="tasks">
  <li class="task">学习 HTML</li>
  <li class="task">学习 CSS</li>
</ul>
```

JavaScript：

```js
const title = document.querySelector("#title");
const firstTask = document.querySelector(".task");
const tasks = document.querySelectorAll(".task");
```

常用：

- `querySelector()`：返回第一个匹配元素。
- `querySelectorAll()`：返回所有匹配元素，结果可遍历。

```js
tasks.forEach((task) => {
  console.log(task.textContent);
});
```

## 4.2 读取和修改内容

```js
const title = document.querySelector("#title");

title.textContent = "新的标题";
```

`textContent` 用于纯文本，安全直接。

```js
const panel = document.querySelector(".panel");
panel.innerHTML = "<strong>重要</strong>";
```

`innerHTML` 会解析 HTML。不要把用户输入直接塞进 `innerHTML`，否则可能产生安全风险。用户输入优先使用 `textContent`。

## 4.3 修改属性和类名

```js
const link = document.querySelector("a");

link.href = "https://developer.mozilla.org/";
link.setAttribute("target", "_blank");
```

类名：

```js
const card = document.querySelector(".card");

card.classList.add("is-active");
card.classList.remove("is-hidden");
card.classList.toggle("is-done");
card.classList.contains("is-active");
```

## 4.4 创建和插入元素

```js
const list = document.querySelector("#taskList");

const item = document.createElement("li");
item.textContent = "学习 JavaScript";
item.classList.add("task-item");

list.append(item);
```

完整函数：

```js
function createTaskElement(title) {
  const item = document.createElement("li");
  item.className = "task-item";
  item.textContent = title;
  return item;
}

const taskElement = createTaskElement("练习 DOM");
document.querySelector("#taskList").append(taskElement);
```

## 4.5 事件

事件是用户或浏览器发生的动作，例如点击、输入、提交、加载。

```js
const button = document.querySelector("#saveButton");

button.addEventListener("click", () => {
  console.log("按钮被点击");
});
```

常见事件：

- `click`：点击。
- `input`：输入内容变化。
- `change`：值改变并确认。
- `submit`：表单提交。
- `keydown`：按下键盘。
- `DOMContentLoaded`：HTML 解析完成。

## 4.6 表单事件

```html
<form id="taskForm">
  <label for="taskInput">任务</label>
  <input id="taskInput" required>
  <button type="submit">添加</button>
</form>

<ul id="taskList"></ul>
```

```js
const form = document.querySelector("#taskForm");
const input = document.querySelector("#taskInput");
const list = document.querySelector("#taskList");

form.addEventListener("submit", (event) => {
  event.preventDefault();

  const title = input.value.trim();
  if (title === "") {
    return;
  }

  const item = document.createElement("li");
  item.textContent = title;
  list.append(item);

  input.value = "";
  input.focus();
});
```

`event.preventDefault()` 阻止表单默认提交刷新页面，让我们用 JavaScript 自己处理。

## 4.7 事件对象

```js
document.addEventListener("keydown", (event) => {
  if (event.key === "Escape") {
    console.log("按下 Escape");
  }
});
```

事件对象常用属性：

- `event.target`：真正触发事件的元素。
- `event.currentTarget`：绑定事件监听的元素。
- `event.key`：键盘按键。
- `event.preventDefault()`：阻止默认行为。
- `event.stopPropagation()`：阻止事件继续冒泡。

## 4.8 事件冒泡与事件委托

事件会从目标元素向外层元素冒泡。

事件委托：把监听器绑在父元素上，根据 `event.target` 判断点击了哪个子元素。

```html
<ul id="taskList">
  <li>
    学习 HTML
    <button data-action="delete">删除</button>
  </li>
</ul>
```

```js
const list = document.querySelector("#taskList");

list.addEventListener("click", (event) => {
  if (event.target.matches("[data-action='delete']")) {
    event.target.closest("li").remove();
  }
});
```

事件委托适合动态生成的列表，因为新添加的按钮也能被父元素监听到。

## 4.9 定时器

```js
const timerId = setTimeout(() => {
  console.log("一秒后执行");
}, 1000);

clearTimeout(timerId);
```

```js
const intervalId = setInterval(() => {
  console.log("每秒执行一次");
}, 1000);

clearInterval(intervalId);
```

## 4.10 异步基础

JavaScript 经常需要等待：

- 等用户点击。
- 等定时器。
- 等网络请求。
- 等文件读取。

Promise 表示“未来会完成或失败的结果”。

```js
const promise = fetch("https://jsonplaceholder.typicode.com/todos/1");

promise
  .then((response) => response.json())
  .then((data) => {
    console.log(data);
  })
  .catch((error) => {
    console.error(error);
  });
```

现代写法更常用 `async` / `await`：

```js
async function loadTodo() {
  try {
    const response = await fetch("https://jsonplaceholder.typicode.com/todos/1");
    const data = await response.json();
    console.log(data);
  } catch (error) {
    console.error("加载失败", error);
  }
}

loadTodo();
```

## 4.11 Fetch API

GET 请求：

```js
async function getTasks() {
  const response = await fetch("/api/tasks");

  if (!response.ok) {
    throw new Error("请求失败");
  }

  return response.json();
}
```

POST 请求：

```js
async function createTask(title) {
  const response = await fetch("/api/tasks", {
    method: "POST",
    headers: {
      "Content-Type": "application/json"
    },
    body: JSON.stringify({ title })
  });

  if (!response.ok) {
    throw new Error("创建失败");
  }

  return response.json();
}
```

注意：

- `fetch()` 只有网络层失败才会进入 `catch`。
- HTTP 404、500 不会自动 throw，需要检查 `response.ok`。

## 4.12 localStorage

`localStorage` 可以在浏览器本地保存字符串数据。

```js
localStorage.setItem("name", "Jeffry");
const name = localStorage.getItem("name");
localStorage.removeItem("name");
```

保存对象或数组要转 JSON：

```js
const tasks = [
  { id: 1, title: "HTML", done: true }
];

localStorage.setItem("tasks", JSON.stringify(tasks));

const saved = localStorage.getItem("tasks");
const parsedTasks = saved ? JSON.parse(saved) : [];
```

适合保存：

- 主题偏好。
- 小型待办事项。
- 草稿。

不适合保存：

- 密码。
- 令牌等敏感信息。
- 很大量的数据。

## 4.13 URL 和查询参数

```js
const url = new URL(window.location.href);
const search = url.searchParams.get("q");
```

生成查询参数：

```js
const params = new URLSearchParams({
  q: "html",
  page: "1"
});

console.log(`/search?${params.toString()}`);
```

## 4.14 模板渲染思路

当数据变成页面时，常见流程：

1. 准备数据。
2. 清空容器。
3. 遍历数据。
4. 每条数据创建 DOM。
5. 插入容器。

```js
const tasks = [
  { id: 1, title: "HTML", done: true },
  { id: 2, title: "CSS", done: false }
];

function renderTasks() {
  const list = document.querySelector("#taskList");
  list.innerHTML = "";

  for (const task of tasks) {
    const item = document.createElement("li");
    item.textContent = task.title;
    if (task.done) {
      item.classList.add("is-done");
    }
    list.append(item);
  }
}
```

## 4.15 状态驱动页面

简单项目也可以用“状态驱动”思路：

```js
let tasks = [];

function addTask(title) {
  tasks.push({
    id: Date.now(),
    title,
    done: false
  });

  saveTasks();
  renderTasks();
}
```

关键原则：

- 数据是事实来源。
- 页面是数据的显示结果。
- 用户操作先改数据，再重新渲染页面。

这样逻辑更清楚，不容易出现“页面显示和数据不一致”。

## 4.16 安全基础

不要把用户输入直接放进 `innerHTML`：

```js
// 危险
container.innerHTML = userInput;
```

更安全：

```js
container.textContent = userInput;
```

如果必须渲染 HTML，需要使用可信来源和严格清理策略。入门阶段记住：用户输入用 `textContent`。

## 4.17 本章练习

练习 1：点击按钮切换深色主题。

```js
const button = document.querySelector("#themeButton");

button.addEventListener("click", () => {
  document.body.classList.toggle("dark");
});
```

练习 2：输入框实时显示字数。

```js
const input = document.querySelector("#message");
const count = document.querySelector("#count");

input.addEventListener("input", () => {
  count.textContent = input.value.length;
});
```

练习 3：用 `localStorage` 保存任务数组，刷新后仍然存在。


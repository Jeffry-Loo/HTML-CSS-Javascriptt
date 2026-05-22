# 第 3 章：JavaScript 语言基础

JavaScript 是网页的编程语言。HTML 写内容，CSS 写样式，JavaScript 写逻辑。

它可以做这些事：

- 根据用户操作改变页面。
- 校验表单输入。
- 从服务器请求数据。
- 保存本地数据。
- 实现复杂交互，例如筛选、拖拽、图表、小游戏。

## 3.1 在 HTML 中引入 JavaScript

推荐：

```html
<script src="app.js" defer></script>
```

`defer` 表示：等 HTML 解析完成后再执行脚本。这样 JavaScript 找页面元素时，元素已经存在。

## 3.2 输出与调试

```js
console.log("Hello JavaScript");
console.warn("这是一条警告");
console.error("这是一条错误");
```

浏览器开发者工具里可以看到这些输出。学习阶段要经常使用 `console.log()` 检查变量。

## 3.3 变量

现代 JavaScript 主要使用 `const` 和 `let`。

```js
const siteName = "前端学习";
let score = 0;

score = score + 1;
```

区别：

- `const`：变量绑定不能重新赋值。
- `let`：可以重新赋值。
- `var`：旧写法，容易产生作用域问题，新代码尽量少用。

注意：`const` 对对象和数组表示“不能换成另一个对象”，不是“内容完全不能改”。

```js
const user = { name: "Jeffry" };
user.name = "Lee"; // 可以

// user = {}; // 不可以
```

## 3.4 数据类型

常见基本类型：

```js
const name = "Jeffry";      // string
const age = 20;             // number
const isStudent = true;     // boolean
const empty = null;         // null
let notSet;                 // undefined
const id = Symbol("id");    // symbol
const big = 123n;           // bigint
```

对象类型：

```js
const user = {
  name: "Jeffry",
  age: 20
};

const skills = ["HTML", "CSS", "JavaScript"];
```

查看类型：

```js
console.log(typeof "hello"); // "string"
console.log(typeof 123);     // "number"
```

## 3.5 字符串

```js
const firstName = "Jeffry";
const message = `Hello, ${firstName}!`;
```

模板字符串使用反引号，可以插入变量，也可以换行。

常用方法：

```js
const title = "  Learn JavaScript  ";

console.log(title.trim());
console.log(title.toLowerCase());
console.log(title.includes("Java"));
console.log(title.replace("JavaScript", "CSS"));
```

## 3.6 数字与运算

```js
const total = 10 + 5;
const diff = 10 - 5;
const product = 10 * 5;
const quotient = 10 / 5;
const remainder = 10 % 3;
const power = 2 ** 3;
```

常用工具：

```js
Math.round(4.6); // 5
Math.floor(4.9); // 4
Math.ceil(4.1);  // 5
Math.max(1, 8, 3);
Math.random();
```

把字符串转数字：

```js
Number("42");
parseInt("42px", 10);
parseFloat("3.14");
```

## 3.7 布尔值与比较

```js
const isDone = false;
const age = 18;

console.log(age >= 18); // true
```

常用比较：

```js
1 === 1;  // true
1 !== 2;  // true
3 > 2;    // true
3 <= 2;   // false
```

建议使用 `===` 和 `!==`，少用 `==` 和 `!=`。严格比较更清楚，不会悄悄转换类型。

逻辑运算：

```js
const canRegister = age >= 18 && isDone === false;
const needsHelp = age < 18 || isDone === false;
const opposite = !isDone;
```

## 3.8 条件语句

```js
const score = 82;

if (score >= 90) {
  console.log("优秀");
} else if (score >= 60) {
  console.log("及格");
} else {
  console.log("继续努力");
}
```

三元表达式适合简单条件：

```js
const status = score >= 60 ? "pass" : "fail";
```

`switch` 适合多个固定值：

```js
const role = "admin";

switch (role) {
  case "admin":
    console.log("管理员");
    break;
  case "user":
    console.log("普通用户");
    break;
  default:
    console.log("访客");
}
```

## 3.9 数组

```js
const skills = ["HTML", "CSS", "JavaScript"];

console.log(skills[0]);      // HTML
console.log(skills.length);  // 3
```

常用方法：

```js
skills.push("React");
skills.pop();
skills.includes("CSS");
skills.join(", ");
```

遍历：

```js
for (const skill of skills) {
  console.log(skill);
}
```

数组高阶方法：

```js
const numbers = [1, 2, 3, 4];

const doubled = numbers.map((number) => number * 2);
const even = numbers.filter((number) => number % 2 === 0);
const sum = numbers.reduce((total, number) => total + number, 0);
const found = numbers.find((number) => number > 2);
```

理解：

- `map`：把每一项变成新值。
- `filter`：筛选符合条件的项。
- `reduce`：累积成一个结果。
- `find`：找到第一个符合条件的项。

## 3.10 对象

对象用来描述一个东西。

```js
const task = {
  id: 1,
  title: "学习 HTML",
  done: false
};

console.log(task.title);
console.log(task["done"]);
```

修改：

```js
task.done = true;
task.priority = "high";
delete task.priority;
```

对象解构：

```js
const { title, done } = task;
```

数组对象很常见：

```js
const tasks = [
  { id: 1, title: "HTML", done: true },
  { id: 2, title: "CSS", done: false },
  { id: 3, title: "JavaScript", done: false }
];
```

筛选未完成任务：

```js
const activeTasks = tasks.filter((task) => !task.done);
```

## 3.11 函数

函数把一段逻辑封装起来。

```js
function greet(name) {
  return `Hello, ${name}`;
}

console.log(greet("Jeffry"));
```

箭头函数：

```js
const add = (a, b) => {
  return a + b;
};
```

简写：

```js
const add = (a, b) => a + b;
```

函数设计建议：

- 一个函数只做一件清楚的事。
- 函数名用动词开头，如 `createTask`、`renderList`。
- 输入靠参数，输出靠 `return`。

## 3.12 作用域

作用域决定变量在哪里可用。

```js
const globalName = "外部";

function test() {
  const localName = "内部";
  console.log(globalName); // 可以
}

// console.log(localName); // 不可以
```

`let` 和 `const` 有块级作用域：

```js
if (true) {
  const message = "hello";
}

// console.log(message); // 不可以
```

## 3.13 模块

当代码变多，可以拆成模块。

```html
<script type="module" src="app.js"></script>
```

`math.js`：

```js
export function add(a, b) {
  return a + b;
}
```

`app.js`：

```js
import { add } from "./math.js";

console.log(add(2, 3));
```

模块默认是严格模式，并且有自己的作用域。

## 3.14 错误处理

```js
try {
  const data = JSON.parse("{ bad json }");
  console.log(data);
} catch (error) {
  console.error("解析失败", error);
}
```

常见错误类型：

- `SyntaxError`：语法错误。
- `ReferenceError`：使用了不存在的变量。
- `TypeError`：类型不对，比如对 `null` 调方法。

## 3.15 JSON

JSON 是常见数据交换格式。

```js
const user = {
  name: "Jeffry",
  age: 20
};

const text = JSON.stringify(user);
const parsed = JSON.parse(text);
```

注意：JSON 的键和字符串必须用双引号。

```json
{
  "name": "Jeffry",
  "age": 20
}
```

## 3.16 本章练习

练习 1：写一个函数 `calculateTotal(items)`，接收商品数组，返回总价。

```js
const items = [
  { name: "Book", price: 30 },
  { name: "Pen", price: 5 }
];
```

参考：

```js
function calculateTotal(items) {
  return items.reduce((total, item) => total + item.price, 0);
}
```

练习 2：从任务数组中筛选未完成任务。

```js
const tasks = [
  { title: "HTML", done: true },
  { title: "CSS", done: false },
  { title: "JS", done: false }
];

const activeTasks = tasks.filter((task) => !task.done);
```

练习 3：写一个函数，判断密码是否至少 8 位，并且包含数字。

```js
function isStrongPassword(password) {
  return password.length >= 8 && /\d/.test(password);
}
```


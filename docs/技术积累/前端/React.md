## DOM

> 这里补充一个常识

**DOM** 全称 **Document Object Model**（文档对象模型）。
 它是 **浏览器把网页内容映射成的一棵树状结构**，让你可以用代码（JS）去读、改网页。

##### 举个例子

假设有一个网页：

```html
<html>
  <body>
    <h1>Hello</h1>
    <p>World</p>
  </body>
</html>
```

浏览器会在内存里建一棵树：

```
Document
 └─ html
     └─ body
         ├─ h1 ("Hello")
         └─ p ("World")
```

这棵树就是 **DOM 树**。

1. **DOM 不是 HTML 本身**

   - HTML 是写在文件里的文本。
   - 浏览器读取 HTML → 解析 → 在内存里生成 DOM 对象。

2. **DOM 是可以操作的**
    你能用 JS 操作 DOM，比如：

   ```js
   document.getElementById("title").innerText = "Hi!";
   ```

   会把页面上某个元素文字改掉。

3. **DOM 是动态的**
    网页不是一成不变的静态文本，JS 改 DOM → 页面立即更新。

- **HTML**：网页的“源代码”，写死的。
- **DOM**：浏览器解析出来的“网页对象树”，可操作的。
- **JS**：通过 DOM API 来修改网页。

React 的核心工作就是：
 **用虚拟 DOM（JS 对象）对比真实 DOM，决定最少的更新，把变化同步到浏览器 DOM 上。**



## 构建 React 开发环境

React 提供了一个官方工具 Create React App，用于快速搭建 React 项目。

create-react-app 是来自于 Facebook，通过该命令我们无需配置就能快速构建 React 开发环境。

create-react-app 自动创建的项目是基于 Webpack + ES6 。

执行以下命令创建项目：

```shell
$ cnpm install -g create-react-app
$ create-react-app my-app
$ cd my-app/
$ npm start
```

> 也可以使用 **npx** 命令来创建，npx 是 npm 5.2.0 及更高版本中包含的一个工具，用于执行本地或远程的 npm 包：
>
> ```
> npx create-react-app my-app
> ```

在浏览器中可以打开 **http://localhost:3000/** 

项目的目录结构如下：

```
my-first-react-app/
├── node_modules/
├── public/
│   ├── favicon.ico
│   ├── index.html
│   ├── logo192.png
│   ├── logo512.png
│   ├── manifest.json
│   └── robots.txt
├── src/
│   ├── App.css
│   ├── App.js
│   ├── App.test.js
│   ├── index.css
│   ├── index.js
│   ├── logo.svg
│   ├── reportWebVitals.js
│   └── setupTests.js
├── .gitignore
├── package.json
├── README.md
└── yarn.lock (或 package-lock.json)
```

### 1 目录和文件说明

```
node_modules/
```

存放所有项目的依赖包。这个目录由 npm 或 yarn 自动生成，包含了项目运行所需的所有第三方库和模块。

```
public/
```

存放静态文件，Webpack 不会对这个目录中的文件进行处理。`public` 目录下的文件会被直接复制到构建目录。

- `favicon.ico`：浏览器标签页上的小图标。
- `index.html`：HTML 模板文件，React 组件将被挂载到这个文件中的 `div` 元素中。
- `logo192.png` 和 `logo512.png`：不同尺寸的 React logo 图标。
- `manifest.json`：Web 应用清单文件，用于定义应用的名称、图标等元数据。
- `robots.txt`：用于告诉搜索引擎哪些页面可以被抓取。

```
src/
```

存放应用的源代码。这里是你主要进行开发的地方。

- `App.css`：`App` 组件的样式文件。
- `App.js`：主组件文件，定义了一个基础的 React 组件。
- `App.test.js`：`App` 组件的测试文件。
- `index.css`：全局样式文件。
- `index.js`：应用的入口文件，负责渲染 React 组件到 DOM 中。
- `logo.svg`：React logo 的 SVG 文件。
- `reportWebVitals.js`：用于性能监测的文件，可以帮助你了解和分析应用的性能。
- `setupTests.js`：用于设置测试环境的文件。

```
.gitignore
```

列出 Git 应该忽略的文件和目录，例如 `node_modules/` 和构建输出的目录。

```
package.json
```

项目的配置文件，包含项目信息、脚本、依赖项等。

```
README.md
```

项目的自述文件，包含项目的基本信息和使用说明。

**`yarn.lock` **或 **`package-lock.json`**

锁定文件，记录了确切的依赖版本，确保在不同环境中安装的依赖一致。

### 2 一些简单的理解

> [!tip]
>
> 这里有一些直观的理解：
>
> ##### 1. React 项目的初始化结构
>
> 典型结构大概是：
>
> ```
> my-app/
> │── public/            # 静态资源（不会被打包修改，直接拷贝到最终产物）
> │    └── index.html    # 唯一的 HTML 模板
> │
> │── src/               # 我们写代码的地方
> │    ├── index.js/tsx  # 程序入口（类似 Python 的 main）
> │    ├── App.js/tsx    # 主组件
> │    ├── components/   # 你自己写的小组件们
> │    └── ...
> │
> │── package.json       # 项目配置、依赖清单
> ```
>
> ##### 2. 谁是“主程序”？
>
> 在 React 里没有 `main()` 函数，但有个 **入口文件**，就是 `src/index.js`（或 `index.tsx`）。这在里面你会看到类似代码：
>
> ```js
> import React from 'react';
> import ReactDOM from 'react-dom/client';
> import App from './App';
> 
> const root = ReactDOM.createRoot(document.getElementById('root'));
> root.render(<App />);
> ```
>
> 这里的逻辑：
>
> 1. **找到 `public/index.html` 中的 `<div id="root"></div>`**
>     （这个 div 就是 React 占领的地方，HTML 只有一个壳）
> 2. **把 `<App />` 这个组件挂进去**
>     React 就从这里开始渲染一整棵组件树。
>
> 所以可以说：
>
> - `index.js` ≈ Python 里的 `main.py`
> - `App.js` ≈ 你写的第一个“顶层类”
>
> ##### 3. 组件关系
>
> React 的世界里，一切都是 **组件**。
>
> - `App.js` 是根组件（树的根）。
> - 你写的 `Header.js`, `Footer.js`, `TodoItem.js` … 都是子组件。
> - 在 `App.js` 里引入它们：
>
> ```js
> import Header from './components/Header';
> import Footer from './components/Footer';
> 
> function App() {
>   return (
>     <div>
>       <Header />
>       <p>Hello World</p>
>       <Footer />
>     </div>
>   );
> }
> ```
>
> 这就是典型的父（App）包含子（Header/Footer）的关系。
>
> ##### 4. 之后要怎么写？
>
> 一般流程是：
>
> 1. **从 App.js 开始**：把页面的整体框架搭出来。
> 2. **拆分组件**：页面上独立的部分（按钮、表单、列表）都写成一个个组件放到 `components/` 文件夹。
> 3. **通过 props 传数据**：父组件把数据传给子组件。
> 4. **通过 state 管理变化**：在需要交互时（比如点击按钮计数），用 `useState`。

## 创建第一个react项目

使用 Create React App 创建一个新的项目。假设你的项目名为 my-app：

```shell
npx create-react-app my-app
```

创建项目后，进入项目目录：

```shell
cd my-app
```

在项目目录中，运行以下命令来启动开发服务器：

```shell
npm start
```

这将启动一个本地开发服务器，并自动在浏览器中打开 http://localhost:3000。你应该会看到一个 React 的欢迎页面。

项目结果如第一小节所述。

### 使用 JSX 语法创建组件

React 组件使用 JSX（JavaScript XML）语法来描述界面结构。

JSX 看起来像 HTML，但它是 JavaScript 的一部分，允许你在组件中直接编写 HTML 标签。

例如，你可以这样创建一个显示个人信息的组件，在 src 目录创建 UserProfile.js 文件，内容如下：

```jsx
import React from 'react';

function UserProfile() {
  const user = {
    name: 'RUNOOB',
    age: 25,
    location: '中国',
  };

  return (
    <div>
      <h2>{user.name}</h2>
      <p>Age: {user.age}</p>
      <p>Location: {user.location}</p>
    </div>
  );
}

export default UserProfile;
```

然后在 App.js 中使用 UserProfile 组件：

```jsx
import React from 'react';
import './App.css';
import UserProfile from './UserProfile'; // 引入组件

function App() {
  return (
    <div className="App">
      <h1>我的第一个 React App!</h1>
      <UserProfile />
    </div>
  );
}

export default App;
```

### 样式与样式文件

React 默认支持 CSS 文件，你可以通过 import './App.css'; 引入样式表来调整应用的外观。

我们也可以使用 CSS 模块 来局部应用样式，或者使用 styled-components 等库进行样式的模块化。

## React 项目说明

一个典型的 React 项目由多个文件和文件夹组成，每个部分都有其特定的作用。

本章节将对 React 项目代码做基本的说明，帮助大家理解项目的结构和各个部分的功能。

- React 项目由多个文件和文件夹组成，核心文件包括 `index.html`、`index.js` 和 `App.js`。
- React 组件是应用的基本构建块，可以是函数组件或类组件。
- JSX 是 React 的核心语法，用于描述 UI。
- Props 和 State 是 React 组件中管理数据的主要方式。

### 项目结构

一个 React 项目通常包含以下文件和文件夹：

```
my-react-app/
├── node_modules/       # 项目依赖的第三方库
├── public/             # 静态资源文件夹
│   ├── index.html      # 应用的 HTML 模板
│   └── ...             # 其他静态资源（如图片、字体等）
├── src/                # 项目源代码
│   ├── App.js          # 主组件
│   ├── App.css         # 主组件的样式
│   ├── index.js        # 项目入口文件
│   ├── index.css       # 全局样式
│   └── ...             # 其他组件和资源
├── package.json        # 项目配置和依赖管理
├── package-lock.json   # 依赖的精确版本锁定文件
└── README.md           # 项目说明文档
```

### 核心文件解析

#### public/index.html

**public/index.html** 是 React 应用的 HTML 模板文件。

React 会将组件渲染到 `<div id="root"></div>` 中。React 会将组件渲染到中。

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>React App</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

#### src/index.js

**src/index.js** 是 React 应用的入口文件。**src/index.js** 负责将根组件（通常是 App）渲染到 index.html 中的 div#root 中。

```js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './index.css';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);
```

#### src/App.js

**src/App.js** 是 React 应用的根组件。**src/App.js** 通常包含应用的主要逻辑和结构。

```js
import React from 'react';
import './App.css';

function App() {
  return (
    <div className="App">
      <h1>Hello, React!</h1>
    </div>
  );
}

export default App;
```

#### src/App.css

**src/App.css** 是 App 组件的样式文件。

```css
.App {
  text-align: center;
  margin-top: 50px;
}
```

#### src/index.css

**src/index.css** 是全局样式文件，通常用于定义全局样式或重置浏览器默认样式。

```css
body {
  margin: 0;
  font-family: Arial, sans-serif;
}
```

#### package.json

**package.json** 这是项目的配置文件，包含项目的元数据、依赖和脚本。

```css
{
  "name": "my-react-app",
  "version": "1.0.0",
  "scripts": {
    "start": "react-scripts start", // 启动开发服务器
    "build": "react-scripts build", // 构建生产环境代码
    "test": "react-scripts test",   // 运行测试
    "eject": "react-scripts eject"  // 弹出配置（高级用法）
  },
  "dependencies": {
    "react": "^18.2.0",
    "react-dom": "^18.2.0",
    "react-scripts": "5.0.1"
  }
}
```

## React 组件的基本结构

React 组件是 React 应用的核心构建块。

一个组件通常包含以下部分：

### 1、函数组件

使用函数定义的组件。

```jsx
import React from 'react';

function MyComponent() {
  return (
    <div>
      <h2>这是一个函数定义的组件</h2>
    </div>
  );
}

export default MyComponent;
```

- **`import React from 'react';`**: 导入了 React 库，React 是一个用于构建用户界面的 JavaScript 库。
- **`function MyComponent() { ... }`**: 这是一个函数组件。函数组件是一个返回 JSX 的 JavaScript 函数。
- **`return (...)`**: 组件的 `return` 语句返回一个 JSX 元素。JSX 是 JavaScript 的语法扩展，允许你在 JavaScript 中编写类似 HTML 的代码。
- **`export default MyComponent;`**: 将 `MyComponent` 组件导出为默认导出。这样，其他文件可以通过 `import MyComponent from './MyComponent';` 来导入并使用这个组件。

### 2、类组件

使用类定义的组件（现在较少使用，推荐使用函数组件）。

```css
import React, { Component } from 'react';

class MyComponent extends Component {
  render() {
    return (
      <div>
        <h2>这是一个类组件</h2>
      </div>
    );
  }
}

export default MyComponent;
```

- **`import React from 'react';`**: 导入 React 库，这是使用 React 的基础。
- **`import { Component } from 'react';`**: 从 React 库中导入 `Component` 类。`Component` 是 React 类组件的基类，所有类组件都需要继承它。
- **`class MyComponent extends Component { ... }`**: 定义了一个名为 `MyComponent` 的类组件。它继承了 `Component` 类，因此可以使用 React 类组件的特性（如生命周期方法、状态管理等）。
- **`render() { ... }`**: `render` 是类组件中必须实现的方法。它负责返回组件的 UI 结构（JSX）。
  - **`return (...)`**: 返回一个 JSX 元素，描述组件的 UI。
  - **`<div><h2>这是一个类组件</h2></div>`**: 这是一个简单的 JSX 结构，包含一个 `div` 和一个 `h2` 标题。
- **`export default MyComponent;`**: 将 `MyComponent` 组件导出为默认导出。这样，其他文件可以通过 `import MyComponent from './MyComponent';` 来导入并使用这个组件。

### 3、JSX

JSX 是 JavaScript 的语法扩展，允许在 JavaScript 中编写类似 HTML 的代码。

### 4、Props

Props 是组件的输入参数，用于从父组件向子组件传递数据。

```jsx
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return <Welcome name="React" />;
}
```

### 5、State

State 是组件的内部状态，用于管理组件的数据。

```jsx
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

## React JSX

React 使用 JSX 来替代常规的 JavaScript。JSX 是一个看起来很像 XML 的 JavaScript 语法扩展。

我们不需要一定使用 JSX，但它有以下优点：

- JSX 执行更快，因为它在编译为 JavaScript 代码后进行了优化。
- 它是类型安全的，在编译过程中就能发现错误。
- 使用 JSX 编写模板更加简单快速。

我们先看下以下代码：

```jsx
const element = <h1>Hello, world!</h1>;
```

这种看起来可能有些奇怪的标签语法既不是字符串也不是 HTML。

它被称为 JSX， 一种 JavaScript 的语法扩展。 我们推荐在 React 中使用 JSX 来描述用户界面。

JSX 是在 JavaScript 内部实现的。

我们知道元素是构成 React 应用的最小单位，JSX 就是用来声明 React 当中的元素。

与浏览器的 DOM 元素不同，React 当中的元素事实上是普通的对象，React DOM 可以确保 浏览器 DOM 的数据内容与 React 元素保持一致。

要将 React 元素渲染到根 DOM 节点中，我们通过把它们都传递给 ReactDOM.render() 的方法来将其渲染到页面上：

```jsx
const element = <h1 className="foo">Hello, world</h1>;
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(element);
```

>注：这个渲染：在你创建了 root 之后，你就可以调用它的 render() 方法，把你整个应用的顶层组件（通常是 <App />）放进去。
>
>通常是这样的：
>
>```js
>// index.js
>import React from 'react';
>import ReactDOM from 'react-dom/client';
>import App from './App'; // 导入你的主组件
>
>// 1. 找到 HTML 中的容器元素
>const container = document.getElementById('root');
>
>// 2. 为这个容器创建一个 React 根
>const root = ReactDOM.createRoot(container);
>
>// 3. 使用 root.render() 方法将你的 React 应用渲染到这个根中
>root.render(
>  <React.StrictMode>
>    <App />
>  </React.StrictMode>
>);
>```

### 使用 JSX

JSX 看起来类似 HTML ，我们可以看下实例:

```jsx
const element = <h1 className="foo">Hello, world</h1>;
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(element);
```

### JavaScript 表达式

我们可以在 JSX 中使用 JavaScript 表达式。表达式写在花括号 **{}** 中。实例如下：

```react
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
    <div>
        <h1>{1+1}</h1>
    </div>
);
```

### 样式

React 推荐使用内联样式。我们可以使用 **camelCase** 语法来设置内联样式. React 会在指定元素数字后自动添加 **px** 。以下实例演示了为 **h1** 元素添加 **myStyle** 内联样式：

```react
var myStyle = {
    fontSize: 100,
    color: '#FF0000'
};
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
    <h1 style = {myStyle}>菜鸟教程</h1>
);
```

### 注释

注释需要写在花括号中，实例如下：

```react
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
    <div>
    <h1>菜鸟教程</h1>
    {/*注释...*/}
    </div>
);
```

### 数组

JSX 允许在模板中插入数组，数组会自动展开所有成员：

```react
var arr = [
  <h1>菜鸟教程</h1>,
  <h2>学的不仅是技术，更是梦想！</h2>,
];
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  <div>{arr}</div>
);
```

## React 组件

React 组件是构建 React 应用的基本单元。

组件可以分为：**函数组件**和**类组件**。

### 函数组件

函数组件是定义组件的一种简洁方法。

函数组件是一个接受 props 并返回 React 元素的 JavaScript 函数。

创建一个简单的函数组件：

```react
import React from 'react';

// 定义一个函数组件
function Welcome(props) {
  return <h1>Hello, {props.name}!</h1>;
}

export default Welcome;
```

在 src/index.js 中渲染该组件：

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import Welcome from './Welcome';

const root = ReactDOM.createRoot(document.getElementById("root"));
// 渲染 Welcome 组件，并传递 name 属性
root.render(<Welcome name="World" />);
```

### 类组件

类组件使用 ES6 类语法定义，通常用于需要管理状态或使用生命周期方法的情况。

创建一个类组件：

```react
import React, { Component } from 'react';

class Welcome extends Component {
  render() {
    return <h1>Hello, {this.props.name}!</h1>;
  }
}

export default Welcome;
```

在 src/index.js 中渲染该组件：

```react
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import Welcome from './Welcome';

const root = ReactDOM.createRoot(document.getElementById("root"));
// 渲染 Welcome 组件，并传递 name 属性
root.render(<Welcome name="World" />);
```

> [!caution]
>
> 因为这是一个 **类**，所以 React 规定必须写一个 `render()` 方法，把要显示的内容返回出来。类组件必须有这个，函数组件没有这个。
>
> 现在不怎么用类组件，基本用函数组件和`hook`就能基本做到所有事。

### 复合组件

```react
function Name(props) {
    return <h1>网站名称：{props.name}</h1>;
}
function Url(props) {
    return <h1>网站地址：{props.url}</h1>;
}
function Nickname(props) {
    return <h1>网站小名：{props.nickname}</h1>;
}
function App() {
    return (
    <div>
        <Name name="菜鸟教程" />
        <Url url="http://www.runoob.com" />
        <Nickname nickname="Runoob" />
    </div>
    );
}
 
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
     <App />
);
```

## React 组件状态(State)

组件可以拥有状态（state），它是组件数据的私有部分，可以用来管理动态数据。

状态仅适用于类组件，或者使用 React 的 Hook 时可以在函数组件中使用。

React 把组件看成是一个状态机（State Machines）。通过与用户的交互，实现不同状态，然后渲染 UI，让用户界面和数据保持一致。

React 里，只需更新组件的 state，然后根据新的 state 重新渲染用户界面（不要操作 DOM）。

以下实例创建一个名称扩展为 React.Component 的 ES6 类，在 render() 方法中使用 this.state 来修改当前的时间。

添加一个类构造函数来初始化状态 this.state，类组件应始终使用 props 调用基础构造函数。

### 类组件中的状态管理

创建一个有状态的类组件：

```react
import React, { Component } from 'react';

class Counter extends Component {
  constructor(props) {
    super(props);
    this.state = { count: 0 };
  }

  increment = () => {
    this.setState({ count: this.state.count + 1 });
  }

  render() {
    return (
      <div>
        <p>Count: {this.state.count}</p>
        <button onClick={this.increment}>Increment</button>
      </div>
    );
  }
}

export default Counter;
```

在 src/index.js 中渲染该组件：

```react
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import Counter from './Counter';

const root = ReactDOM.createRoot(document.getElementById("root"));
// 渲染 Counter 组件
root.render(<Counter />);
```

### 函数组件中的状态管理（使用 Hook）

使用 React Hook 可以在函数组件中使用状态。最常用的 Hook 是 useState。

创建一个有状态的函数组件：

```react
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default Counter;
```

在 src/index.js 中渲染该组件：

```js
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import Counter from './Counter';

const root = ReactDOM.createRoot(document.getElementById("root"));
// 渲染 Counter 组件
root.render(<Counter />);
```



## React Props

在 React 中，Props（属性）是用于将数据从父组件传递到子组件的机制，Props 是只读的，子组件不能直接修改它们，而是应该由父组件来管理和更新。

state 和 props 主要的区别在于 **props** 是不可变的，而 state 可以根据与用户交互来改变。这就是为什么有些容器组件需要定义 state 来更新和修改数据。 而子组件只能通过 props 来传递数据。

### 使用 Props

传递 Props 语法：

```react
<ComponentName propName={propValue} />
```

以下实例演示了如何在组件中使用 props：

```react
function HelloMessage(props) {
    return <h1>Hello {props.name}!</h1>;
}
 
const element = <HelloMessage name="Runoob"/>;
 
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
    element
);
```

### 默认 Props

你可以通过组件类的 defaultProps 属性为 props 设置默认值，实例如下：

```react
class HelloMessage extends React.Component {
  render() {
    return (
      <h1>Hello, {this.props.name}</h1>
    );
  }
}
 
HelloMessage.defaultProps = {
  name: 'Runoob'
};//如果别人用 `<HelloMessage />` 时 **没有传 name 属性**，就用 `'Runoob'` 作为默认值。
 
const element = <HelloMessage/>;
 
const root = ReactDOM.createRoot(document.getElementById("root"));
root.render(
  element
);
```

### 多个 Props

可以传递多个属性给子组件。

```react
const UserCard = (props) => {
  return (
    <div>
      <h2>{props.name}</h2>
      <p>Age: {props.age}</p>
      <p>Location: {props.location}</p>
    </div>
  );
};

const App = () => {
  return (
    <UserCard name="Alice" age={25} location="New York" />
  );
};

ReactDOM.render(<App />, document.getElementById('root'));
```

### 解构 Props

在函数组件中，可以通过解构 props 来简化代码。

```react
const Greeting = ({ name }) => {
  return <h1>Hello, {name}!</h1>;
};

const App = () => {
  return <Greeting name="Alice" />;
};

ReactDOM.render(<App />, document.getElementById('root'));
```



## How to use React

React本质上是一个JSX的使用（当然也可以是TSX），在许多语法要求上与JSX相同，但是更加严格，这里简单举几个例子

### 1 严格的闭合标签

所有的标签必须有闭合，且一个函数只能返回一个大标签下的内容(这意味着你最好在每一个组件的return中都默认带上空白标签对作为大标签

```TypeScript
function App(){
    return(
    <>
        <h1>hello</h1>
        <br/>next
    </>);
}
```

### 2 组件导出

```TypeScript
function MyComponent() {
  return (
    <div>
      <h1>Hello, World!</h1>
      <p>This is a React component.</p>
    </div>
  );
}

export default MyComponent;
```

这个时候就可以导出MyComponent作为别的组件内的"标签"了

```TypeScript
import MyComponent from './MyComponent';

function App() {
  return (
    <div>
      <h1>Welcome to my React App!</h1>
      <MyComponent />
    </div>
  );
}

export default App;
```

- 注意:React标签必须是大写字母开头的

### 3 事件响应

```TypeScript
function MyButton() {
  function handleClick() {
    alert('You clicked me!');
  }

  return (
    <button onClick={handleClick}>
      Click me
    </button>
  );
}
```

- 此时对于Click事件,我们给出了回应handClick

### 4 组件状态

在 React 中，我们通常使用 state 来存储组件的状态，而不像 js 那样随意定义各种变量。这是因为 React 重新渲染组件时不会保留组件内的局部变量，修改这些变量也不会触发重新渲染。

存储和修改 state 需要用到`useState`，这是一个 React 钩子，它接收状态的初始值，返回当前状态以及更新状态的函数

```TypeScript
const [index, setIndex] = useState(0);
setIndex(index + 114514);
```

- 记得 import

### 5 传递参数

React 组件使用 *props* 来互相通信。每个父组件都可以提供 props 给它的子组件，从而将一些信息传递给它。

state 和 props 主要的区别在于 **props** 是不可变的，而 state 可以根据与用户交互来改变。这就是为什么有些容器组件需要定义 state 来更新和修改数据。 而子组件只能通过 props 来传递数据。

>```react
>function Child(props) {
>return <p>Hello, {props.name}!</p>;
>}
>
>function Parent() {
>return <Child name="Alice" />;
>}
>```
>
>简单理解以下，parent里面调用了child，那parent就是父组件，child就是子组件。然后child可以通过props调用父组件的信息，但这个不可以改变。

**props传递步骤**

**步骤一：将 props 传递给子组件**

首先，将一些 props 传递给 `Avatar`。例如，让我们传递两个 props：`person`（一个对象）和 `size`（一个数字）：

```JavaScript
export default function Profile() {
  return (
    <Avatar
      person={{ name: 'Lin Lanying', imageId: '1bX5QH6' }}
      size={100}
    />
  );
}
```

**步骤二：在子组件中读取 props**

你可以通过在 `function Avatar` 之后直接列出它们的名字 `person, size` 来读取这些 props。这些 props 在 `({` 和 `})` 之间，并由逗号分隔。这样，你可以在 `Avatar` 的代码中使用它们，就像使用变量一样。

```JavaScript
function Avatar({ person, size }) {
  // 在这里 person 和 size 是可访问的
}
```

**使用 JSX 展开语法传递 props**

有时候，传递 props 会变得非常重复：

```JavaScript
function Profile({ person, size, isSepia, thickBorder }) {
  return (
    <div className="card">
      <Avatar
        person={person}
        size={size}
        isSepia={isSepia}
        thickBorder={thickBorder}
      />
    </div>
  );
}
```

重复代码没有错（它可以更清晰）,但我们可以进行简化：

```JavaScript
function Profile(props) {
  return (
    <div className="card">
      <Avatar {...props} />
    </div>
  );
}
```

这会将 `Profile` 的所有 props 转发到 `Avatar`，而不列出每个名字。

**注意：请克制地使用展开语法**！

interface作为props

```JavaScript
export interface MessageProps {
    messageId: number;
    roomId: number;
    sender: string;
    content: string;
    time: number;
    user: string;
}

export function MessageItem (props: MessageProps) {

}
```

### 6 map方法

在React中，`map` 方法是数组的一个常用方法，用于遍历数组并对数组中的每个元素进行操作，返回一个新的数组。它在React中常用于渲染列表组件，将数组中的数据映射为一组React元素。

1. **基本用法**

`map` 方法会遍历数组中的每个元素，并对每个元素执行传入的回调函数，然后将回调函数的返回值组成一个新的数组返回。

语法：

```JavaScript
array.map((item, index, array) => {// 对每个元素进行操作return something;});
```

- `item`：当前遍历到的元素
- `index`：当前元素的索引（可选）
- `array`：当前正在遍历的数组（可选）
- React中使用`map` 渲染列表

假设我们有一个用户列表数据，需要在React组件中渲染成一个列表：

```JavaScript
import React from 'react';
const users = [{ id: 1, name: 'Alice', age: 25 },
                { id: 2, name: 'Bob', age: 30 },
                { id: 3, name: 'Charlie', age: 35 }];
const UserList = () => {
    return (
        <div>
            <h1>User List</h1>
            <ul>{users.map((user) => (
                <li key={user.id}>{user.name} - {user.age}</li>
                )
            )}</ul>
        </div>
      );
};
export default UserList;
```

代码解析：

1. **数据准备**：`users` 是一个数组，包含多个用户对象。
2. 使用`map`方法：
   1. `users.map((user) => ...)`：遍历`users`数组，对每个用户对象执行回调函数。
   2. 回调函数返回一个`<li>`元素，显示用户的`name`和`age`。
   3. 每个`<li>`元素通过`key`属性设置了唯一的标识（`user.id`），这是React渲染列表时推荐的做法，以提高性能和避免渲染错误。
3. **渲染结果**：
   1. 最终，`map`方法返回一个由`<li>`元素组成的数组，React会将这些元素渲染到`<ul>`中。
4. **注意事项**

- **`key`**属性：在使用`map`渲染列表时，React要求每个列表项有一个唯一的`key`属性。`key`可以是数组元素的唯一标识（如`id`），帮助React高效地更新和管理列表项。
- **返回值**：`map`方法的回调函数必须有返回值，否则返回的数组中会包含`undefined`。
- **不修改原数组**：`map`方法不会修改原数组，而是返回一个新的数组。
- **更复杂的场景**

假设我们有一个更复杂的对象数组，需要对每个对象的某些属性进行操作后渲染：

```JavaScript
import React from 'react';
const products = 
[{ id: 1, name: 'Apple', price: 10, inStock: true },
{ id: 2, name: 'Banana', price: 5, inStock: false },
{ id: 3, name: 'Orange', price: 8, inStock: true }];
const ProductList = () => {
    return (
        <div>
            <h1>Product List</h1>
            <ul>{products.map((product) => (
                <li key={product.id}>
                {product.name} - ${product.price}
                {product.inStock ? <span> (In Stock)</span> : <span> (Out of Stock)</span>}
                </li>
                ))}
                </ul>
        </div>
     );
};
export default ProductList;
```



> 这里本来应该有很多类组件的介绍，但是现在我们对类组件使用较少，所以暂时在此处掠过。



## React Hooks

React Hooks 是 React 16.8 引入的一项重要特性，它使函数组件能够拥有类组件的一些特性，例如状态管理和生命周期方法的使用。

通过 Hooks，可以更加简洁和灵活地编写 React 组件。

### 概述

#### 1. 什么是 React Hooks？

React Hooks 是一种函数式组件的增强机制，它允许你在不编写类组件的情况下使用 React 的特性。主要的 Hooks 包括 `useState`, `useEffect`, `useContext`, `useReducer`, `useCallback`, `useMemo`, `useRef`, 和 `useImperativeHandle` 等。这些 Hooks 提供了访问 React 特性的方式，使得你可以更好地组织和重用你的代码。

#### 2. 主要的 React Hooks

`useState` Hook 允许你在函数组件中使用局部状态。它返回一个状态值和更新该状态值的函数。

```react
import React, { useState } from 'react';

function Counter() {
  const [count, setCount] = useState(0);

  return (
    <div>
      <p>You clicked {count} times</p>
      <button onClick={() => setCount(count + 1)}>Click me</button>
    </div>
  );
}
```

`useEffect` Hook 允许你在函数组件中执行副作用操作（如数据获取、订阅管理、DOM 操作等）。它在每次渲染后都会执行。

```react
import React, { useState, useEffect } from 'react';

function Timer() {
  const [seconds, setSeconds] = useState(0);

  useEffect(() => {
    const interval = setInterval(() => {
      setSeconds(seconds => seconds + 1);
    }, 1000);  //渲染后，每隔1000ms就会对seconds进行+1

    return () => clearInterval(interval);
  }, []); // 空数组作为第二个参数表示仅在组件挂载和卸载时执行

  return <p>Timer: {seconds} seconds</p>;
}
```

以下是一些主要的 React Hooks 及其用途：

**useState** - 用于在函数组件中添加 state，你可以使用它来跟踪随时间变化的数据。

```react
const [state, setState] = useState(initialState);
```

**useEffect** - 用于执行副作用操作，比如数据获取、订阅或手动更改 DOM，它与类组件中的 componentDidMount、componentDidUpdate 和 componentWillUnmount 生命周期类似。

```react
useEffect(() => {
  // 执行副作用操作
  return () => {
    // 清理操作
  };
}, [dependencies]); // 依赖数组
```

**useContext** - 用于访问 React context 在组件树中传递的数据，而不必通过每个组件传递 props。

```react
const value = useContext(MyContext);
```

**useReducer** - 用于更复杂的 state 逻辑，它接收一个 reducer 函数和初始状态，然后返回当前的状态和派发 action 的 dispatch 函数。

```react
const [state, dispatch] = useReducer(reducer, initialState);
```

**useCallback** - 用于返回一个 memoized 版本的回调函数，防止不必要的渲染。

```react
const memoizedCallback = useCallback(
  () => {
    // 回调函数体
  },
  [dependencies] // 依赖数组
);
```

**useMemo** - 用于对计算结果进行记忆，避免在每次渲染时重复计算。

```react
const memoizedValue = useMemo(() => computeExpensiveValue(a, b), [a, b]);
```

**useRef** - 用于创建对 DOM 元素或值的引用，可以在渲染之间保持状态。

```react
const refContainer = useRef(initialValue);
```

**useImperativeHandle** - 用于使用 ref 时暴露 DOM 元素的方法。

```react
useImperativeHandle(ref, () => ({
  // 暴露的方法
}));
useLayoutEffect - 与 useEffect 类似，但它在所有的 DOM 变更之后同步执行。这在需要读取 DOM 布局并同步触发重渲染时非常有用。

useLayoutEffect(() => {
  // 副作用操作
}, [dependencies]);
```

**useDebugValue** - 用于在 React 开发者工具中显示自定义 hook 的标签。

```react
useDebugValue(value);
```

#### 3. 使用 React Hooks 的好处

- **更简洁的组件逻辑**：无需编写类组件，可以使用函数组件和 Hooks 来管理状态和生命周期。
- **提高代码复用性**：Hooks 可以帮助你将逻辑提取到可重用的函数中，减少重复代码。
- **更好的性能优化**：使用 `useEffect`, `useCallback`, `useMemo` 等 Hooks 可以更精确地控制副作用和性能消耗。

#### 4. 注意事项

- **仅在顶层使用 Hooks**：不要在循环、条件或嵌套函数中调用 Hook，确保 Hooks 在每次渲染时都以相同的顺序被调用。
- **使用 ESLint 插件**：React 官方提供了 eslint-plugin-react-hooks 插件来帮助你检查 Hook 的使用是否正确。

#### 5. 实例

以下是一个使用多个 React Hooks 的示例：



### react hooks 详解

#### 1 Class component vs. Function component

在 React 中，一个常见的写法是使用 class component:                                                                                         

```JavaScript
class MyConponent extends React.Component {
    // state 状态
    constructor(props) {
        super(props);
        this.state = {counts: 0};
    }
    clickHandle() {
        this.setState({
          counts: this.state.counts++
        });
    }
    // 生命周期函数
    componentDidMount() {
        console.log('Did mouned!');
    }
    render() {
        return (
            <>
                <div>
                  Counts: {this.state.counts}
                </div>
                <button onClick={this.clickHandle}>+1</button>
            </>
        );
    }
}
```

在 Hooks 推出之前，在 React 中使用状态（state）、生命周期方法（lifecycle methods）、上下文（context）等等重要 React 特性的唯一方法就是通过 **class component**。所以在当时，类定义组件是编写 React 组件的标准方法。我们虽然可以用函数编写组件，但是它必须是一个**纯函数（Pure function）**，所以我们没法使用状态等功能。

**纯函数（Pure function）**指的是仅依赖于传入的参数且不会对外界造成副作用的函数。

随着 Hooks 在 React v16.8 版本中正式推出，**函数式组件（function component）**成为了编写组件的最佳实践。Hooks 意为“钩子”，指的是可以在函数内部把外部状态和功能“钩”进来。借助 hooks 我们可以在保持组件为纯函数的情况下使用状态、副作用等等功能。

```JavaScript
function MyConponent ()  {
    const [counts, setCounts] = useState(0);
    return (
        <>
            <div>
                Counts: {counts}
            </div>
            <button onClick={() => setCount(count + 1)}>+1</button>
        </>
    );
};
```

所以，现在在 React 中实现组件有两种方式，class component 与 function component。相比较下，class component 存在很多缺点，包括但不限于：

1. `this` 指代不明；
2. 难以复用、拆分、重构和测试；
3. 引入了复杂的 render props、高阶组件等；

为了解决这些问题，hooks 使你在非 class 的情况下可以使用更多的 React 特性。

#### 2 为什么是函数？

这不得不提一下 React 的设计理念。从概念上来说，React 把组件视为一个输入数据输出 UI 视图的函数。所以函数式的组件更符合其设计理念，同时可以避开 class component 的很多缺点。

React 团队希望让 Hooks 能够覆盖所有之前 class component 的使用场景，但目前并不会放弃对 class component 的支持。两种方式可以在一起使用。

##### 有哪些 hook

最基本的 hooks：

- useState（状态）
- useEffect（副作用）
- useContext（上下文）

高级 hooks：

- useRef
- useCallback
- useReducer
- useMemo
- ……

不难发现，React 中的 hooks 都是由 `use` 开头。除此之外，我们还可以定义自己的 [custom hooks](https://reactjs.org/docs/hooks-custom.html)。

本文主要介绍较为常见的几个 hooks。

#### 3 useState

在 class component 中，我们一般会写这样的代码：

```JavaScript
class example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {counts: 0};
  }
};
```

这里我们在构造函数中定义了 `this.state`，也就是这个组件的状态。之后我们就可以读取/修改 `this.state` 的值了。使用 `setState()` 更新状态时，React 就能获知状态发生改变，从而重新渲染页面。

那么在 function component 中怎么使用 state hook 来实现这个功能呢？

```JavaScript
import React, { useState } from 'react'; // 导入

function example(props) {
  const [counts, setCounts] = useState(0);
  function handleClick() {
    setCounts(counts + 1);
  }
  return (
    <>
      <div>
        Counts: {counts}
      </div>
      <button onClick={handleClick}>
        +1
      </button>
    </>
  );
}
```

可以发现，`useState()` 接受一个参数作为输入，其意义为**初始状态**；返回一个长度为 2 的数组，分别是**当前的状态**以及**更新状态的函数**。

所以在这个例子中，我们使用 hook 定义了 `counts` 这个状态，初始为 0。修改 `counts` 的函数为 `setCounts()`。之后，可以直接读取 `counts` 的值，并通过 `setCounts()` 更新状态。

##### 注意事项

使用 `useState` 时有几个需要注意的地方：

- **永远不要**直接对某个状态进行赋值，比如在上面的例子里直接写 `counts = counts + 1` 是不可以的。
- Class component 的 `setState()` 函数在更新对象（object）时是默认合并的，但是 state hook 的状态更新函数是**默认替换的**。如果想要实现对象合并的效果，记得使用展开运算符 `...`。
- 只能在 function component 中使用 hooks。
- 在 v18 版本后，React 会在尽量不产生错误的前提下，批量同步执行相邻的状态更新操作以减少 re-render 次数，提升性能。具体请见 [Automatic batching for fewer renders in React 18](https://github.com/reactwg/react-18/discussions/21)。

##### 浅试一下

看看这个计时器的例子：

```JavaScript
// example 1
function App() {
  const [count, setCount] = useState(0);
  
  function startCountdown() {
    setInterval(() => {
      setCount(count + 1);
    }, 1000);
  }
  
  return (
    <div>
      <div>Count: {count}</div>
      <button onClick={startCountdown}>Start countdown</button>
    </div>
  );
}
```

我们预期的结果是，点击按钮，计数器从 0 开始每秒加一。但事实是什么样的呢？

如果你熟悉 JS，那么聪明的你肯定会发现，这是由闭包引起的问题。Interval 中的 `count` 值始终保持为定义 Interval 那个时刻的值不变。React hooks 重度依赖闭包，所以在开发时，一定要考虑到闭包带来的问题。

那么怎么解决呢？一种解决方案是，把上面的 `setCount(count + 1);` 改为 `setCount(count => count + 1);`。这样做等于是告诉 hook 我们想要的是把状态 `count` 的值递增 1，而并不依赖于原来的 `count` 值，也就避免了闭包带来的错误。（但这个写法依然存在不合理的地方，比如 `setInterval` 其实是一个会造成副作用的操作，应当把它写在 useEffect 当中。）

#### 4 useReducer

它是一个高级钩子，可以帮助我们更好地管理状态。我们在这里简单讲讲使用的方法。

```JavaScript
const [state, dispatch] = useReducer(reducer, initialArg, init);
```

其实可以把 `useReducer` 看作是更高级的 `useState`。

参数中第一个 `reducer` 是一个函数；`initialArg` 是状态的初始值计算函数的参数；`init` 是计算状态初始值的函数，可以直接留空。留空表示状态的初始值就是 `initialArg`，否则初始值就是 `init(initialArg)`。

一般的简单写法是：

```JavaScript
const [state, dispatch] = useReducer(reducer, initialState);
```

`useReducer` 的返回值也是一个数组，第一项是状态 `state`，第二项是调度函数 `dispatch`。

`reducer` 是一个**纯函数**。它接受两个参数——当前状态和行动对象，并返回一个参数——更新后的状态。`dispatch` 函数用于调度，它接受一个参数——行动对象。

##### 示例

```JavaScript
function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return {count: state.count + 1};
    case 'decrement';
      return {count: state.count - 1};
    default:
      throw new Error();
  }
}

function Counter() {
  const [state, dispatch] = useReducer(reducer, {count: 0});
  return (
    <>
      Count: {state.count}  //感觉这个dispatch就是相当于要通知下一步要干什么，相当于dispatch(action)这样
      <button onClick={() => dispatch({type: 'decrement'})}>-1</button> 
      <button onClick={() => dispatch({type: 'increment'})}>+1</button>
    </>
  );
}
```

和 `useState` 相比，`useReducer` 多了一个 `reducer` 函数，并且把 `setState` 改为了 `dispatch`。这实际上把状态的维护逻辑进行了一层封装。

我们把可能对状态进行的操作写在 `reducer` 中，并在行动对象中标识操作、附带参数。比如在这个例子中，我们有 `increment` 和 `decrement` 两种操作。根据 `action.type` 的不同，`reducer` 做出相应的处理，并返回新的状态。

这样我们通过调度函数 `dispatch(action)` 就可以按照指定的信息进行状态的修改。调用 `dispatch({type: 'increment'})` 就可以让 `state.count` 递增 1。 

##### 注意事项

- `reducer` 必须是一个**纯函数**。
- `reducer` 中，不能直接对状态进行修改或赋值。应当创建一个新的对象，并在进行必要修改后返回。这里需要注意深浅拷贝问题。可以善用解构赋值。
- React 会保证 `dispatch` 函数在组件存在时保持不变。

#### 5 useEffect

本文重点介绍对象—— `useEffect`。

之前我们提到，函数式组件应当是一个没有副作用的纯函数。但通过 Effect hook，我们可以实现副作用操作。它的格式是这样的：

```JavaScript
useEffect(effect, deps);
```

其中 `effect` 是一个**函数**，它不接受参数。这个函数内部就是具体的副作用操作，譬如网络请求、设置订阅、DOM 操作等等。同时，这个函数可以有返回值，返回值依然是一个不接受参数的函数，表示对副作用的清理或消除。`deps` 可以是 `undefined` 或者一个**可以为空的数组**，表示这个副作用的依赖。

这样似乎难以理解。我们可以试着这样思考：

组件在渲染时可能希望产生某些副作用，如修改 DOM，访问网络等。我们使用 effect hook 来实现这个功能——把副作用写在 `useEffect` 的参数当中。而在**每次重新渲染**时，这些副作用都会被重新执行，这会引入一些问题：

- 有时我们希望在重新执行副作用之前消除前一次副作用。解决的办法是在 `effect` 参数中写上返回值。
- 有时某些副作用的重复执行是不必要的且可能影响性能。解决办法就是为副作用加入依赖项。这样做其实是在告诉 React：“这个副作用只依赖于这些值，如果这些值没有改变，那就没有必要重复执行副作用”。那么 React 在每次重新渲染时，就会把每个副作用的依赖项与上次渲染时的值进行比较。当有值发生了改变时，React 才会重新执行副作用。如果依赖项为 undefined，那么每次 re-render 时都会执行副作用。

React 在比较依赖项时，使用的是**浅比较**。所以尽量不要把整个对象、数组等直接作为依赖项。

##### 示例

我们来看看之前 state hook 中使用过的计时器例子，但这次我们使用 `useEffect` 钩子。

```JavaScript
// example 2
function App() {
  const [count, setCount] = useState(0);
  
  useEffect(() => {
    const interval = setInterval(() => {
      setCount(count + 1);
    }, 1000);
    return () => {clearInterval(interval);}
  }, [count]);
  
  return (
    <div>
      <div>Count: {count}</div>
    </div>
  );
}
```

尝试理解一下这段代码。

- 第一次渲染时，执行副作用。设置了一个定时器，每隔一秒递增一次 `count`。
- 第一秒过去后，`count` 加 1。状态改变触发 re-render。
- 重新渲染后比较副作用的依赖。发现 `count` 值发生了改变。
- 重新执行副作用。执行时分为两步。
  - 首先，清除上一次的副作用。可以看到代码中定义了清除副作用的函数——它清除了定时器。
  - 然后，执行这一次的副作用。也就是重新设置了定时器。它将在 1 秒后给 `count` 加 1。
- ……

所以，这段代码通过不太直接的方式实现了一个秒数计时器。

##### 状态"快门"

我们看一下这个更为直观的例子：

```JavaScript
// example 3
function App() {
  const [count, setCount] = useState(0);
  
  function addCount() {
    setCount(count + 1);
  }
  
  useEffect(() => {
    setTimeout(() => {
      console.log(count);
    }, 5000);
  }, [count]);
  
  return (
    <div>
      <button onClick={addCount}>+1</button>
    </div>
  );
}
```

尝试快速地点击多次 +1 按钮，然后查看 console。每次打印的值符合你的预期吗？

我们可以认为，每一次渲染，React 都生成了一个当前组件的“副本”。对于一个“副本”来说，里面的所有 states 都是不可改变的常量（这就是我们为什么使用 `const` 来定义 state）；但是不同的“副本”之间，这些 states 可能有所不同。而每一个“副本”中的 effects，只能获取到它所在的“副本”中的 states。

在上面的例子中，第一次点击 +1 按钮后，React 进行一次重新渲染，并产生了一个“副本”。在这个“副本”当中，`count` 的值为 1。然后 React 执行副作用，设置了一个定时器，在 1 秒后打印 `count` 的值。而 1 秒后，不论你点击了多少次 +1 按钮，`count` 的值对于这个“副本”来说，值始终都是 1。

这样的性质对于 class component 并**不成立**。如果你感兴趣的话，可以实现一个看似等价的组件，[执行一下](https://codepen.io/deluxurousCodePen/pen/GRGRbqY)看看效果。

事实上，不只有 states 和 effects，“副本”中所有的函数（自定义函数、计时器等等）都会捕获它所在的那次渲染中的 states 和 props，而这些 states 和 props 对于他们所在的“副本”来说都是常量。这也解释了为什么不能对 states 直接赋值。

闭包的无处不在可能会使你感到厌恶，但好处在于，闭包使得每次渲染时的逻辑清晰且确定。

如果你不想要这种效果，而想要像 class component 那样读取当前实际状态的值，可以使用 `useRef`，我们会在后文讲到。

你或许在之前学过一些这样的东西：

> *【教程】如何使用 useEffect 模拟 class component 的生命周期*

> ```JavaScript
> useEffect(() => {
>   ...
> }, []);
> ```
>
> *这样可以让这个副作用在组件 mount 时执行一次，实现 componentDidMount 的效果。*

事实是，class component 的思维模型并不能完全同样地应用于 hooks，上面的写法也不能保证 100% 符合期望。想要更好的理解和使用 useEffect，需要进行一些思维的转换。一个建议是，把生命周期的概念**都忘掉**，试着去用 effects 的方式思考。

#### 6 useRef

Ref 意为引用。通过 `useRef` 我们可以创建一个引用。

```JavaScript
const ref = useRef(initialValue);
```

创建的方式很简单，`useRef` 接收一个参数，作为这个引用的初始值。

值的获取和修改也很简单：

```JavaScript
console.log(ref.current);
ref.current = nextValue;
```

通过 `.current` 直接进行访问和修改即可。

我们来看一下这个例子：

```JavaScript
// example 5
function App() {
  const [count, setCount] = useState(0);
  const cntRef = useRef(0);
  
  function addCount() {
    setCount(count + 1);
    cntRef.current ++;
  }
  
  useEffect(() => {
    setTimeout(() => {
      console.log("State: " + count + "; Ref: " + cntRef.current);
    }, 2000);
  }, [count]);
  
  return (
    <div>
      <div>Count: {count}</div>
      <button onClick={addCount}>+1</button>
    </div>
  );
}
```



## SWR

SWR 是由 [Next.js](https://nextjs.org/)（React 框架）背后的同一团队创建的**用于数据请求的 React Hooks 库。**

“SWR” 这个名字来自于 `stale-while-revalidate`：一种由 [HTTP RFC 5861](https://tools.ietf.org/html/rfc5861) 推广的 HTTP 缓存失效策略。这种策略首先从缓存中返回数据（过期的），同时发送 fetch 请求（重新验证），最后得到最新数据。

### 特性

使用 SWR，组件将会**不断地**、**自动**获得最新数据流。 UI 也会一直保持**快速响应**。

- 通过 key 去除重复的请求，做到请求缓存和共享
- 在用户重新 focus 网页和网络重连时自动重新请求数据、自动定期重新请求
- 允许请求依赖其他动态数据，确保最大程度的并行性和串行请求
- 使用指数退避算法的错误重试，不会浪费资源频繁地重试
- UI的乐观更新与错误回滚
- 数据预请求和预填充

大部分特性可以自定义开启或者关闭。

### 安装

在 React 项目目录运行以下命令：

```Plaintext
yarn add swr
```

或者用 npm:

```Plaintext
npm install swr
```

### 基本使用

为了开始使用 SWR，我们需要先理解几个概念：

1. SWR 使用 key 来标识一个请求，这个 key 可以是（通常是）请求的路径，也可以是路径与 token 的组合，可以是一个数组，可以是一个对象。SWR 将深度地对比（递归地在每一层级都按值比较判断相等）这个 key，若 key 发生了变化，则会重新触发请求。
2. SWR 需要一个 fetcher 来进行请求。这个 fetcher 函数可以使用任意其他的请求方式，比如原生的 fetch，比如 axios 等等。以下是 fetcher 函数示例：

```JavaScript
// fetch (GET)
const fetcher = url => fetch(url).then(r => r.json())
// axios (GET)
const fetcher = url => axios.get(url).then(res => res.data)
```

### 核心 Hook 语法

```JavaScript
const { data, error, isLoading, isValidating, mutate } = useSWR(key, fetcher, options)
```

参数:

- `key`: 请求的唯一 key。类型为 string（或者是 function / array / null） [(详情)](https://swr.bootcss.com/docs/arguments.html), [（高级用法）](https://swr.bootcss.com/docs/conditional-fetching.html)
- `fetcher`:*（可选）*一个根据 key 请求对应的数据的函数 [（详情）](https://swr.bootcss.com/docs/data-fetching.html)
- `options`:（*可选）*该 SWR hook 的配置参数

默认情况下，`key` 将作为参数传递给 `fetcher`。所以下面 1) 2) 这 2 个表达式是等价的：

```JavaScript
// 定义 fetcher
function fetcher(key) {
  return fetch(key).then(resp => resp.json());
}

useSWR('/api/user', url => fetcher(url))   // 1)
useSWR('/api/user', fetcher)               // 2)
```

你也可以不提供 fetcher，SWR 内部默认将会使用浏览器提供的 fetch 函数（来自 Fetch API）作为 fetcher：

```JavaScript
const { data, error, isLoading } = useSWR('/api/versions/')

if (isLoading)
    return <Loading />
if (error)
    return <Error reason={error.message}>
```

#### 返回值

- `data`: 通过 `fetcher` 用给定的 key 获取的数据（如未完全加载，返回 undefined）
- `error`: `fetcher` 抛出的错误（或者是 undefined）
- `isLoading`: 是否有一个正在进行中的请求且当前没有“已加载的数据“。预设数据及之前的数据不会被视为“已加载的数据“
- `isValidating`: 是否有请求或重新验证加载
- `mutate(data?, options?)`: 更改缓存数据的函数 [（详情）](https://swr.bootcss.com/docs/mutation.html)

### 使用实例

#### 基础用法

```JavaScript
import useSWR from "swr";

const fetcher = (...args) => fetch(...args).then((res) => res.json())

function Profile() {
  const { data, error, isLoading } = useSWR("/api/user/123", fetcher)
  if (error) return <div>failed to load</div> 
  if (isLoading) return <div>loading...</div>  
  
  // 渲染数据  
  return <div>hello {data.name}!</div>
}
```

这里的 `fetcher` 是一个异步函数，它 **接受** SWR 的 **`key`** 并返回数据。

返回值将作为 `data` 传递，如果抛出错误，将作为 `error` 被捕获。

#### 避免逻辑隔离后重复请求

通常情况下我们会在父组件请求一次数据，然后将数据拆分之后通过 props 传递给子组件中，或者使用 [React Context](https://legacy.reactjs.org/docs/context.html) 进行数据分发。一旦整个页面的深度增加，整个逻辑就会变得冗杂。

```JavaScript
// 页面组件

function Page() {
  const [user, setUser] = useState(null)

  // 请求数据
  useEffect(() => {
    fetch("/api/user")
      .then((res) => res.json())
      .then((data) => setUser(data))
  }, [])

  // 全局加载状态
  if (!user) return <Spinner />

  return <div>
    <Navbar user={user} />
    <Content user={user} />
  </div>
}

// 子组件

function Navbar({ user }) {
  return <div>
    ...
    <Avatar user={user} />
  </div>
}

function Content({ user }) {
  return <h1>Welcome back, {user.name}</h1>
}

function Avatar({ user }) {
  return <img src={user.avatar} alt={user.name} />
}
```

而如果我们使用 SWR，就可以很方便地将每个数据都 **绑定** 在需要这个数据的子组件上，每个组件相互独立，父组件不需要关心数据或者数据传递，父组件只需要关心他的本职工作——渲染子组件即可。

```JavaScript
// 封装好的 useUser hook
function useUser() {
  const { data, mutate, error } = useSWR("api_user", userFetcher);

  const loading = !data && !error;
  const loggedOut = error && error.status === 403;

  return {
    loading,
    loggedOut,
    user: data,
    mutate
  };
}


// 页面组件

function Page() {
  return <div>
    <Navbar />
    <Content />
  </div>
}

// 子组件

function Navbar() {
  return <div>
    ...
    <Avatar />
  </div>
}

function Content() {
  const { user, isLoading } = useUser()
  if (isLoading) return <Spinner />
  return <h1>Welcome back, {user.name}</h1>
}

function Avatar() {
  const { user, isLoading } = useUser()
  if (isLoading) return <Spinner />
  return <img src={user.avatar} alt={user.name} />
}
```

一般来讲，这么做虽然可以使得整个逻辑变得清晰，但是代价就是整个数据会被请求多次！但是由于 SWR 搭载的 key 机制，使得以上代码虽然调用了两次`useUser`，却只有 **1个请求** 发出，因为这两个`useUser`使用的 key 是相同的，请求会被自动地去除重复、缓存和共享！

这使得你可以在任何地方重用数据 hooks 而不必担心请求重复发生。

#### 错误重试

在出现错误时 SWR 使用指数退避算法重发请求。该算法允许应用从错误中快速恢复，而不会浪费资源频繁地重试。

可以通过配置 options 中的 [onErrorRetry](https://swr.bootcss.com/docs/api.html#options) 选项覆盖该行为：

```JavaScript
useSWR('/api/user', fetcher, {
  onErrorRetry: (error, key, config, revalidate, { retryCount }) => {
    // 404 时不重试。
    if (error.status === 404) return

    // 特定的 key 时不重试。
    if (key === '/api/user') return

    // 最多重试 10 次。
    if (retryCount >= 10) return

    // 5秒后重试。
    setTimeout(() => revalidate({ retryCount: retryCount }), 5000)
  }
})
```

这个回调让你可以灵活的根据各种条件重试。你也可以通过设置 `shouldRetryOnError: false` 来禁用它。

#### 数据依赖、条件请求

有的时候，我们需要根据前一个请求获取到的数据来拼装出下一个请求的 URL 或者请求体。一个朴素的想法是使用 `if` 来包裹或者限制 `useSWR`：

```TypeScript
function Profile() {
  const {
    data: user,
    isLoading: isUserLoading,
    error: fetchUserError
  } = useSWR('/api/user/get');  // 通过 Cookie 来获取当前 user

  if (isUserLoading) return <Loading />;
  if (fetchUserError) return <Error message={fetchUserError.message} />;
  
  const { data: avatarUrl, isLoading, error } = useSWR('/api/avatar/get/' + user.id);
  
  if (isLoading) return <Loading />
  if (error) return <Error message={error.message} />;
  
  return <img src={avatarUrl} alt={user.name} />
}
```

但是，如果你仔细阅读过 [React Hooks](https://xn4zlkzg4p.feishu.cn/wiki/wikcnAj97pK5WexPjxFZ3AUEWRc) 的「**禁忌事项**」章节，那么就应当知道：这样是完全不正确的，甚至可能导致你的整个组件的状态直接崩掉。

正确的做法有以下两种：

#### 条件请求

```JavaScript
function Profile() {
  const {
    data: user,
    isLoading: isUserLoading,
    error: fetchUserError
  } = useSWR('/api/user/get');  // 通过 Cookie 来获取当前 user
  const { data: avatarUrl, isLoading, error } = useSWR(
    isUserLoading ? null : '/api/avatar/get/' + user.id  // (1)
  );

  if (isUserLoading || isLoading) return <Loading />;
  if (fetchUserError) return <Error message={fetchUserError.message} />;
  if (error) return <Error message={error.message} />;
  
  return <img src={avatarUrl} alt={user.name} />
}
```

注意，在 `(1)` 这一行，我们在前置数据没准备好时，传给 `useSWR` 的 key 是 `null`。那么这个时候 SWR 库就会知道前置数据还没准备好，而把对应的 `isLoading` 直接设置为 `true`，直到 key 从 `null` 改变为某个字符串。





## 路由

### 前言

如果我们希望做一个SPA（单页面应用），那路由是绕不开的话题。而React Router是react官方（FaceBook）维护的路由库。

React Router随着react的迭代更新推出了多个版本，现在已经到了v6。而目前react router也向着react的迭代大潮进发，全面地转向了hooks。

React Router 有着多个针对不同开发环境的包，比如react-router(核心包，更兼容、更繁琐)、react-router-dom（适合web开发）、react-router-native（适合react native）。

本文只阐述react-router-dom的相关知识。

### 安装

```Shell
npm install react-router-dom
```

### 基本使用

#### 1 添加一个路由器

React Routor提供了多种路由器，我们常见的有：

- [BrowserRouter](https://reactrouter.com/en/main/router-components/browser-router)（通常使用）
  - 内部靠HTML5的History实现
  - 由于背靠History，页面刷新之后路由中的state仍然会保留
- [HashRouter](https://reactrouter.com/en/main/router-components/hash-router)
  - 兼容性非常好
  - url中会携带‘#’

如果我们希望开始使用React Router来制作路由的话，那我们必须选择一种路由器来包裹我们需要使用到路由功能的其他==所有HTML元素==，不然路由无法正确跳转（实际表现是console报错）。我们通常的做法就是在我们的`<App ``/``>`外侧用路由器进行包裹。

我们以BroserRouter为例：

```JavaScript
import ReactDOM from 'react-dom'
import * as React from 'react'
import { BrowserRouter } from 'react-router-dom'
import App from './App'

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
, document.getElementById('app))
```

实际上你也可以紧跟潮流使用函数式组件的特色——hook来完成这个事情——[createBrowserRouter v6.8.1](https://reactrouter.com/en/main/routers/create-browser-router)。

（React Router作为官方的路由库，自然紧跟react函数式组件的潮流）

#### 2 第一个路由

```JavaScript
function App() {
  return (
    <Routes>
      <Route path="/home" element={<Home />} />
    </Routes>
  );
}
```

- <Routes>组件：如果你需要使用<Route>，那你必须使用<Routes>来包裹他们（注意他们拼写上的区别！），这个组件将会负责从他包裹的<Route>中挑选匹配当前path的路由并加载
- <Route>组件：React Router的最重要组件。用来注册一个路由。当path匹配成功后，将会渲染element属性中的组件。
  - path：该路由的路径
  - element: 匹配到之后所渲染的组件

#### 3 更多的路由（匹配规则）

```JavaScript
function App() {
 return (
   <Routes>
     <Route path="/home" element={<Home />} />
     <Route path="/profile" element={<Profile />} />
     {/* more <Route /> */}
   </Routes>
 );
}
```

Route将会按照如下规则进行匹配

- 按照Route标签排布的先后顺序匹配
- 假设当前传入的路由是'/path/to/something'，该路由将匹配<Route path="/path">，匹配<Route path="/path/to">等等

#### 4 嵌套路由

接下来我们要做的是添加层级更高的路由，这样我们就可以做到二级路由了

```JavaScript
function App() {
 return (
   <Routes>
     <Route path="/home" element={<Home />} />
     <Route path="/profile" element={<Profile />}>
       <Route path="me" element={<OthersProfile />} />
     </Route>
     {/* more <Route /> */}
   </Routes>
 );
}
```

以第6行为例：

当我们访问`ip:port/profile/me`的时候，就会同时渲染Profile组件和OtherProfile组件，而这个`me`就是二级路由。（当然路由可以有三级四级等等）

请注意Route中的path属性：'path'和'/path'的写法是不同的，前者是相对写法，后者是绝对写法（类似相对路径和绝对路径）

实际上你也可以紧跟潮流使用函数式组件的特色——hook来完成这个事情——[useRoutes v6.8.1](https://reactrouter.com/en/main/hooks/use-routes)。

#####  Outlet

当你使用二级路由的时候，需要在一级路由的element中放置<Outlet>组件来标识你的二级路由匹配到的element放置在何处。（类似于占位符）

以上方的代码为例，那么我们在Profile组件中就需要添加Outlet来放置'profile/me'匹配到的OtherProfile组件

```JavaScript
function Profile() {
  return (
    <div>Profile</div>
    <Outlet />
 );
}
```

#### 5 切换路由的组件

##### Link

Link的实际表现类似于<a>标签，其中的'to'就是'herf'，支持相对路径和绝对路径两种写法。

```JavaScript
function EditContact() {
    <Link to="/">
      Cancel
    </Link>
  );
}
```

##### NavLink

是一个特殊的`<Link />`组件，常用于渲染导航栏选中时的高亮。

我们可以将其className写成一个函数来接收一个参数，调整其被选中之后的样式

```TypeScript
<NavLink className={({isActive: boolean}) => isActive ? '各种className' : '各种className'}>
  home
</NavLink>
```

#### 6 路由传递参数

##### Params

```JavaScript
function App() {
 return (
   <Routes>
     <Route path="/home" element={<Home />} />
     <Route path="/profile" element={<Profile />}>
       <Route path=":id" element={<OthersProfile />} />
     </Route>
     {/* more <Route /> */}
   </Routes>
 );
}
```

你可以在定义路由的时候使用`:paramName`来指定需要接收的参数。上方的diamante就定义了一个名为`id`的param

然后你在对应路由的组件（上方代码中就是OtherProfile）中就可以使用useParams这个hook来获得传递的值

```JavaScript
import {useParams} from 'react-router-dom'
function OtherProfile() {
  const {id} = useParams();
  return (
   <div>接收到的参数是:{id}</div>
  );
}
```

至于如何跳转到'/profile/1'这样的路由，你可以使用Link或者NavLink等。

##### SearchParams

SearchParams本质上就是在正常的路由后面跟上'?'以及多个参数的urlencoded编码，例如：

> /detail?id=1&title='Hello'&content='World'

你可以使用useSearchParams这个hook来解析上方这个路由

```JavaScript
import {useSearchParams} from 'react-router-dom'
function OtherProfile() {
  const {search,setSearch} = useSearchParams();
  const id = search.get('id');
  const title = search.get('title');
  const content = search.get('content')
  return (
   <div>接收到的参数是:{id},{title},{content}</div>
  );
}
```

##### State

你可以在Link中直接添加State来储存参数

```JavaScript
function EditContact() {
    <Link to="/"
     state={{
        id:1,
        title:'Hello',
        content:'World'
     }}
    >
      Cancel
    </Link>
  );
}
```

然后使用useLocation这个hook来获得传过来的state

```JavaScript
import {useLocation} from 'react-router-dom'
function OtherProfile() {
  const {state:{id,title,content}} = useLocation();
  return (
   <div>接收到的参数是:{id},{title},{content}</div>
  );
}
```

#### 7 编程操控路由导航

借助useNavigate这个hook即可手动操作路由的跳转。

```JavaScript
import {useNavigate} from 'react-router-dom'

function test() {
    const navigate = useNavigate();
    navigate('subRoute') /*跳转到子路由subRoute*/
    navigate('/home') /*跳转到/home*/
    navigate(1)/*前进->*/
    navigate(-1)/*后退<-*/
}
```


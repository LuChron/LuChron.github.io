## NPM 使用介绍

NPM（Node Package Manager）是一个 JavaScript 包管理工具，也是 Node.js 的默认包管理器。

NPM 允许开发者轻松地下载、安装、共享、管理项目的依赖库和工具。

NPM 是 Node.js 自带的包管理工具，因此，通常你只需安装 Node.js，NPM 就会自动安装在系统中。

**主要功能：**

- **包管理**：NPM 可以帮助你安装并管理项目所需的各种第三方库（包）。例如，可以通过简单的命令来安装、更新、或删除依赖。
- **版本管理**：NPM 支持版本控制，允许你锁定某个特定版本的依赖，或根据需求选择最新的版本。
- **包发布**：NPM 允许开发者将自己的库发布到 NPM 仓库中，其他开发者可以通过 NPM 下载并使用这些库。
- **命令行工具**：NPM 提供了强大的命令行工具，可以用于安装包、运行脚本、初始化项目等多种操作。

由于新版的 Node.js 已经集成了 NPM，所以我们可以直接通过输入 **npm -v** 来测试是否成功安装，出现版本提示表示安装成功:

```shell
$ npm -v
2.3.0
```

------

## 使用 npm 命令安装模块

npm 安装 Node.js 模块语法格式如下：

```shell
$ npm install <Module Name>
```

以下实例，我们使用 npm 命令安装常用的 Node.js web框架模块 **express**:

```shell
$ npm install express
```

安装好之后，express 包就放在了工程目录下的 node_modules 目录中，因此在代码中只需要通过 **require('express')** 的方式就好，无需指定第三方包路径。

```js
var express = require('express');
```

------

## 全局安装与本地安装

npm 的包安装分为本地安装（local）、全局安装（global）两种，从敲的命令行来看，差别只是有没有 **-g** 参数。

**本地安装：**将包安装到 node_modules 目录，并将信息保存到 package.json 的 dependencies 中。

```shell
npm install express          # 本地安装
```

**全局安装：**用于安装命令行工具或需要在多个项目中使用的包。

```shell
npm install express -g   # 全局安装
```

如果出现以下错误：

```shell
npm err! Error: connect ECONNREFUSED 127.0.0.1:8087 
```

解决办法为：

```shell
$ npm config set proxy null
```

### 本地安装

- **作用范围**：默认情况下，npm 会将包安装在当前项目的 `node_modules` 文件夹中。这意味着每个使用该包的项目都会有自己的包副本。
- **用途**：本地安装通常用于项目依赖。每个项目可以有自己的依赖版本，这有助于确保项目的稳定性和可复现性。
- **安装命令**：在项目目录中运行 `npm install <package-name>` 会将包安装在 `node_modules` 文件夹中，并在 `package.json` 文件中添加依赖项。
- **版本管理**：通过 `package.json` 和 `package-lock.json` 文件管理依赖的版本，确保项目在不同环境中的一致性。

### 全局安装

- **作用范围**：全局安装会将包安装在系统级别的目录中，通常是 `/usr/local/bin`（在 Unix-like 系统上）或 `%AppData%\npm`（在 Windows 上）。
- **用途**：全局安装用于那些不需要在每个项目中重复安装的工具或命令行实用程序。例如，安装一个全局的 `create-react-app` 可以用于创建新的 React 项目。
- **安装命令**：使用 `-g` 标志来全局安装包，例如 `npm install -g <package-name>`。
- **版本管理**：全局安装的包版本由 npm 管理，但不会在项目的 `package.json` 中体现。这意味着全局安装的包可能在不同项目之间共享，但也可能因为版本冲突而导致问题。

| 特性         | 本地安装                          | 全局安装                      |
| :----------- | :-------------------------------- | :---------------------------- |
| **安装范围** | 仅在当前项目中可用                | 在系统的全局环境中可用        |
| **命令使用** | `npm install package-name`        | `npm install -g package-name` |
| **安装位置** | `node_modules` 目录               | 系统全局目录（依 OS 而异）    |
| **使用场景** | 项目依赖（库、框架）              | CLI 工具、项目生成器          |
| **访问方式** | 通过 `require()` 或 `import` 使用 | 在命令行中直接使用            |
| **依赖声明** | 在 `package.json` 中记录          | 不在 `package.json` 中记录    |
| **版本控制** | 不同项目中可用不同版本            | 系统中只保留一个版本          |
| **权限问题** | 无需特殊权限                      | 可能需要管理员权限            |

如果你希望具备两者功能，则需要在两个地方安装它或使用 **npm link**。

接下来我们使用全局方式安装 express

```shell
$ npm install express -g
```

安装过程输出如下内容，第一行输出了模块的版本号及安装位置。

```shell
express@4.13.3 node_modules/express
├── escape-html@1.0.2
├── range-parser@1.0.2
├── merge-descriptors@1.0.0
├── array-flatten@1.1.1
├── cookie@0.1.3
├── utils-merge@1.0.0
├── parseurl@1.3.0
├── cookie-signature@1.0.6
├── methods@1.1.1
├── fresh@0.3.0
├── vary@1.0.1
├── path-to-regexp@0.1.7
├── content-type@1.0.1
├── etag@1.7.0
├── serve-static@1.10.0
├── content-disposition@0.5.0
├── depd@1.0.1
├── qs@4.0.0
├── finalhandler@0.4.0 (unpipe@1.0.0)
├── on-finished@2.3.0 (ee-first@1.1.1)
├── proxy-addr@1.0.8 (forwarded@0.1.0, ipaddr.js@1.0.1)
├── debug@2.2.0 (ms@0.7.1)
├── type-is@1.6.8 (media-typer@0.3.0, mime-types@2.1.6)
├── accepts@1.2.12 (negotiator@0.5.3, mime-types@2.1.6)
└── send@0.13.0 (destroy@1.0.3, statuses@1.2.1, ms@0.7.1, mime@1.3.4, http-errors@1.3.1)
```

### 查看安装信息

你可以使用以下命令来查看所有全局安装的模块：

```shell
$ npm list -g

├─┬ cnpm@4.3.2
│ ├── auto-correct@1.0.0
│ ├── bagpipe@0.3.5
│ ├── colors@1.1.2
│ ├─┬ commander@2.9.0
│ │ └── graceful-readlink@1.0.1
│ ├─┬ cross-spawn@0.2.9
│ │ └── lru-cache@2.7.3
……
```

如果要查看某个模块的版本号，可以使用命令如下：

```shell
$ npm list grunt

projectName@projectVersion /path/to/project/folder
└── grunt@0.4.1
```

------

## 卸载模块

我们可以使用以下命令来卸载 Node.js 模块。

```shell
$ npm uninstall express
```

卸载后，你可以到 /node_modules/ 目录下查看包是否还存在，或者使用以下命令查看：

```shell
$ npm ls
```

------

## 更新模块

我们可以使用以下命令更新模块：

```shell
$ npm update express
```

------

## 搜索模块

使用以下来搜索模块：

```shell
$ npm search express
```

------

## 创建模块

创建模块，package.json 文件是必不可少的。我们可以使用 NPM 生成 package.json 文件，生成的文件包含了基本的结果。

>什么是packeage.json ？
>
>`package.json` 是 **Node.js/前端项目的核心配置文件**，相当于项目的“说明书 + 依赖清单”。类似`requirements.txt`
>
>放在项目根目录里，一般长这样：
>
>```json
>{
>  "name": "my-app",
>  "version": "1.0.0",
>  "scripts": {
>    "dev": "next dev",
>    "build": "next build",
>    "start": "next start"
>  },
>  "dependencies": {
>    "next": "14.2.3",
>    "react": "18.2.0",
>    "react-dom": "18.2.0"
>  },
>  "devDependencies": {
>    "typescript": "^5.3.3",
>    "prisma": "^6.14.0"
>  }
>}
>```
>
>1. **项目元信息 (metadata)**
>
>   - `name`: 项目名字
>   - `version`: 版本号
>   - 作者、许可证等等
>
>2. **依赖管理**
>
>   - `dependencies`: 运行项目时需要的库（生产环境也要用）
>   - `devDependencies`: 只在开发时需要的库（类型文件、测试工具、编译器等）
>
>3. **脚本 (scripts)**
>
>   - 定义常用命令，简化操作。
>      比如：
>
>   ```shell
>   pnpm run dev   # 实际执行 next dev
>   pnpm run build # 实际执行 next build
>   ```
>
>4. **配置 (config)**
>
>   - 有些库（比如 ESLint、Prettier、Jest）可以直接在 `package.json` 里放配置。
>
>更具体内容请见后文。

```shell
$ npm init
This utility will walk you through creating a package.json file.
It only covers the most common items, and tries to guess sensible defaults.

See `npm help json` for definitive documentation on these fields
and exactly what they do.

Use `npm install <pkg> --save` afterwards to install a package and
save it as a dependency in the package.json file.

Press ^C at any time to quit.
name: (node_modules) runoob                   # 模块名
version: (1.0.0) 
description: Node.js 测试模块(www.runoob.com)  # 描述
entry point: (index.js) 
test command: make test
git repository: https://github.com/runoob/runoob.git  # Github 地址
keywords: 
author: 
license: (ISC) 
About to write to ……/node_modules/package.json:      # 生成地址

{
  "name": "runoob",
  "version": "1.0.0",
  "description": "Node.js 测试模块(www.runoob.com)",
  ……
}


Is this ok? (yes) yes
```

以上的信息，你需要根据你自己的情况输入。在最后输入 "yes" 后会生成 package.json 文件。

接下来我们可以使用以下命令在 npm 资源库中注册用户（使用邮箱注册）：

```shell
$ npm adduser
Username: mcmohd
Password:
Email: (this IS public) mcmohd@gmail.com
```

接下来我们就用以下命令来发布模块：

```shell
$ npm publish
```

如果你以上的步骤都操作正确，你就可以跟其他模块一样使用 npm 来安装。

## 版本号

使用 NPM 下载和发布代码时都会接触到版本号，NPM 使用语义版本号来管理代码，这里简单介绍一下。

版本号遵循语义化版本控制（SemVer），格式为 MAJOR.MINOR.PATCH，并可附加额外标记。

- **MAJOR（主版本）**：当你做了不兼容的 API 改动时增加。例如：`2.0.0`。
- **MINOR（次版本）**：当你添加新功能但保持向后兼容时增加。例如：`1.1.0`。
- **PATCH（补丁版本）**：当你修复 bug 而不增加新功能时增加。例如：`1.0.1`。

### 额外标记

- **预发布版本**：如 `1.0.0-alpha` 或 `1.0.0-beta.1`，表示该版本仍在测试中。
- **构建元数据**：如 `1.0.0+build.1`，提供有关构建的信息。

### 安装示例

- 安装特定版本：`npm install package-name@1.2.3`
- 安装最新的主版本：`npm install package-name@^1.2.3` （安装 `1.x.x` 的最新版本）

------

## NPM 常用命令

NPM 提供了很多命令，可以使用 **npm help** 可查看所有命令。

| 命令                                  | 说明                                                       |
| :------------------------------------ | :--------------------------------------------------------- |
| `npm init`                            | 初始化一个新的 `package.json` 文件，交互式输入信息。       |
| `npm init -y`                         | 快速创建带有默认设置的 `package.json` 文件。               |
| `npm install package-name`            | 本地安装指定包。                                           |
| `npm install -g package-name`         | 全局安装指定包，使其在系统范围内可用。                     |
| `npm install`                         | 安装 `package.json` 中列出的所有依赖。                     |
| `npm install package-name --save-dev` | 安装包并添加到 `devDependencies`。                         |
| `npm update package-name`             | 更新指定的依赖包。                                         |
| `npm uninstall package-name`          | 卸载指定的依赖包。                                         |
| `npm uninstall -g package-name`       | 全局卸载指定的包。                                         |
| `npm list`                            | 查看当前项目的已安装依赖包列表。                           |
| `npm list -g --depth=0`               | 查看全局已安装的依赖包列表（不展开依赖树）。               |
| `npm info package-name`               | 查看包的详细信息，包括版本和依赖等。                       |
| `npm login`                           | 登录到 NPM 账号。                                          |
| `npm publish`                         | 发布当前包到 NPM 注册表。                                  |
| `npm unpublish package-name`          | 从 NPM 注册表中撤销发布的包（一般限 24 小时内）。          |
| `npm cache clean --force`             | 清理 NPM 缓存。                                            |
| `npm audit`                           | 检查项目依赖中的安全漏洞。                                 |
| `npm audit fix`                       | 自动修复已知的漏洞。                                       |
| `npm run script-name`                 | 运行 `package.json` 中定义的脚本，例如 `npm run start`。   |
| `npm start`                           | 运行 `start` 脚本（等同于 `npm run start`）。              |
| `npm test`                            | 运行 `test` 脚本。                                         |
| `npm build`                           | 运行 `build` 脚本。                                        |
| `npm outdated`                        | 列出项目中有可更新版本的依赖包。                           |
| `npm version patch/minor/major`       | 更新 `package.json` 中的版本号，自动更新版本。             |
| `npm ci`                              | 使用 `package-lock.json` 快速安装依赖，适用于 CI/CD 环境。 |

除了本章介绍的部分外，NPM 还提供了很多功能，package.json 里也有很多其它有用的字段。

除了可以在 https://docs.npmjs.com/ 查看官方文档外，这里再介绍一些NPM常用命令。

------

## package.json 的详细说明与使用

package.json 是 Node.js 项目中的一个核心文件，包含了项目的元数据、依赖、脚本等信息。

package.json 文件用于描述项目的元数据和依赖关系，它通常位于项目的根目录中，并且是项目的配置文件。

package.json 文件是一个 JSON 格式的文件，包含以下基本字段：

- `name`：项目的名称，应该是唯一的，通常使用小写字母和连字符。
- `version`：项目的版本号，遵循语义化版本控制（Semantic Versioning）。
- `description`：项目的简短描述。
- `main`：项目的入口文件，通常是应用程序的启动文件。
- `scripts`：定义了一系列的命令行脚本，可以在项目中执行特定的任务。
- `dependencies`：列出了项目运行所需的所有依赖包及其版本。
- `devDependencies`：列出了只在开发过程中需要的依赖包及其版本。
- `peerDependencies`：列出了项目期望其依赖包也依赖的包。
- `optionalDependencies`：列出了可选的依赖包。
- `engines`：指定了项目兼容的 Node.js 版本。
- `repository`：项目的代码仓库信息，如 GitHub 仓库的 URL。
- `keywords`：项目的关键词，有助于在 npm 搜索中找到项目。
- `author`：项目的作者信息。
- `license`：项目的许可证信息。

**使用方法：**

1. **初始化项目**：在项目目录中运行 `npm init` 命令，npm 会引导你创建一个 `package.json` 文件，或者自动生成一个包含默认值的 `package.json`。
2. **安装依赖**：使用 `npm install <package-name>` 命令安装依赖，npm 会自动将依赖添加到 `package.json` 文件的 `dependencies` 或 `devDependencies` 中，并创建 `package-lock.json` 文件以锁定依赖的版本。
3. **管理脚本**：在 `scripts` 字段中定义命令，例如 `"start": "node app.js"`，然后可以通过 `npm start` 命令来运行这些脚本。
4. **版本控制**：使用 `npm version` 命令来管理项目的版本号，npm 会自动更新 `package.json` 中的版本号，并生成一个新的 Git 标签。
5. **发布包**：当项目准备好发布到 npm 时，可以使用 `npm publish` 命令，npm 会读取 `package.json` 中的信息来发布包。
6. **依赖管理**：`package.json` 和 `package-lock.json` 文件一起工作，确保项目在不同环境中的依赖版本一致。

| 字段                | 说明                                                         |
| :------------------ | :----------------------------------------------------------- |
| **name**            | 项目的名称，通常是小写字母和连字符。                         |
| **version**         | 项目的版本号，遵循 [语义化版本规范 (SemVer)](https://semver.org/)。 |
| **description**     | 项目的简短描述。                                             |
| **main**            | 项目的入口文件，默认为 `index.js`。                          |
| **scripts**         | 定义项目可执行的脚本命令，如 `npm start`。                   |
| **dependencies**    | 项目运行时需要的依赖库，会在安装时加入 `node_modules`。      |
| **devDependencies** | 开发时使用的依赖库，不会在生产环境中安装。                   |
| **keywords**        | 关键字数组，有助于描述项目并在 NPM 搜索中找到项目。          |
| **author**          | 项目的作者信息。                                             |
| **license**         | 项目的许可证类型，如 `MIT`、`ISC`。                          |

### 使用 package.json 的好处

- **依赖管理**：集中管理项目的依赖项及其版本。
- **自动化任务**：通过 `scripts` 字段可以方便地运行常见的任务。
- **版本控制**：确保项目及其依赖版本的一致性，便于团队协作。
- **描述项目**：为项目提供元数据信息，便于发布和共享。

一个例子：

```json
{
  "name": "my-project",
  "version": "1.0.0",
  "description": "A simple Node.js project",
  "main": "app.js",
  "scripts": {
    "start": "node app.js",
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "dependencies": {
    "express": "^4.17.1"
  },
  "devDependencies": {
    "nodemon": "^2.0.20"
  },
  "keywords": ["node", "npm", "example"],
  "author": "Your Name",
  "license": "MIT"
}
```

### 依赖管理

**dependencies**：存储项目运行所需的依赖。

```json
"dependencies": {
  "express": "^4.17.1"
}
```

安装依赖时使用：

```shell
npm install express
```

**devDependencies**：存储项目开发期间需要的依赖。

```json
"devDependencies": {
  "nodemon": "^2.0.20"
}
```

安装依赖时使用：

```shell
npm install nodemon --save-dev
```

### scripts 字段

scripts 字段用于定义可通过 npm run <script> 执行的命令。常见的脚本包括：

```json
"scripts": {
  "start": "node app.js",
  "test": "jest",
  "build": "webpack --mode production",
  "dev": "nodemon app.js"
}
```

运行脚本示例：

```shell
npm run dev   # 执行 "nodemon app.js"
npm start     # 等同于 "node app.js"，可以直接用 npm start 运行
```

### 版本号中的符号说明

- **`^`**（插入符）：表示安装与当前主版本兼容的最新版本。例如，`^4.17.1` 会安装 `4.x.x` 中的最新版本。
- **`~`**（波浪号）：表示安装与当前次版本兼容的最新版本。例如，`~4.17.1` 会安装 `4.17.x` 中的最新版本。

### 常用命令

初始化 package.json 文件：

```shell
npm init
```

使用 npm init -y 可以快速生成默认的 package.json 文件。

查看项目依赖：

```shell
npm list --depth=0
```

更新依赖：

```shell
npm update package-name
```

### 注意事项

- 保持 `package.json` 文件的简洁和准确，避免不必要的字段。
- 使用 `package-lock.json` 来锁定依赖的版本，以确保项目在不同环境中的一致性。
- 定期更新依赖，以利用最新的功能和安全修复
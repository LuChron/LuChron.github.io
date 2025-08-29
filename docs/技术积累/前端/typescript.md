## 前言

写在前面：之前学习js的时候不怎么扎实。当时好多没看懂。学习C#之后发现比较好理解了。这里我再系统学习一下typescript。

### JavaScript 与 TypeScript 的区别

TypeScript 是 JavaScript 的超集，扩展了 JavaScript 的语法，因此现有的 JavaScript 代码可与 TypeScript 一起工作无需任何修改，TypeScript 通过类型注解提供编译时的静态类型检查。

TypeScript 可处理已有的 JavaScript 代码，并只对其中的 TypeScript 代码进行编译。

### NPM 安装 TypeScript

如果本地环境已经安装了 [npm](D:\task\note\xlab\前端三大件\NPM.md) 工具，可以使用以下命令来安装。

使用国内镜像：

```
npm config set registry https://registry.npmmirror.com
```

安装 typescript：

```
npm install -g typescript
```

安装完成后我们可以使用 **tsc** 命令来执行 TypeScript 的相关代码，以下是查看版本号：

```
$ tsc -v
Version 3.2.2
```

然后我们新建一个 app.ts 的文件，代码如下：

```ts
var message = "Hello World";
console.log(message);
```

通常我们使用 **.ts** 作为 TypeScript 代码文件的扩展名。

然后执行以下命令将 TypeScript 转换为 JavaScript 代码：

```
tsc app.ts
```

![img](../../assets/图片/typescript_compiler.png)

这时候在当前目录下（与 app.ts 同一目录）就会生成一个 app.js 文件。

使用 node 命令来执行 app.js 文件：

```shell
$ node app.js 
Hello World
```

TypeScript 转换为 JavaScript 过程如下图：

![img](../../assets/图片/ts-2020-12-01-1.png)



## TypeScript 特性

相对 JavaScript，TypeScript 增加了许多关键功能，特别是围绕类型系统和代码结构的增强功能。

TypeScript 的一些关键特性：

- **静态类型检查**：TypeScript 在编译时就会检查代码的类型是否匹配，能够发现很多潜在的错误。即使是简单的错误（例如拼写错误或类型不一致），也可以在编写代码时被捕获到。
- **类型推断**：TypeScript 能够自动推断变量的类型。比如当你声明一个变量并赋值时，TypeScript 会根据赋值来推断这个变量的类型，不需要每次都显式声明类型。
- **接口和类型定义**：TypeScript 提供了 `interface` 和 `type` 关键字，允许你定义复杂的数据结构。这对于项目中不同部分的代码协作和数据交互来说非常重要。
- **类和模块支持**：TypeScript 支持面向对象编程中的类（class）概念，增加了构造函数、继承、访问控制修饰符（如 `public`、`private`、`protected`），并且支持 ES 模块化规范。
- **工具和编辑器支持**：TypeScript 拥有良好的编辑器支持，特别是与 Visual Studio Code 集成时，能提供智能提示、自动补全、重构等工具，使开发过程更高效。
- **兼容 JavaScript**：TypeScript 是 JavaScript 的超集，这意味着所有合法的 JavaScript 代码都是合法的 TypeScript 代码。这使得 JavaScript 项目可以逐步迁移到 TypeScript，而无需完全重写。

以下是 TypeScript 增加的主要功能：

### 1. **静态类型**

TypeScript 的最大特性就是增加了静态类型系统。在 TypeScript 中，开发者可以显式地声明变量、参数、返回值的类型，这样可以在编译时捕获很多潜在的类型错误。常见类型包括 `number`、`string`、`boolean`、`array`、`tuple`、`enum` 等，此外也支持自定义类型。

```ts
let name: string = "Alice";
let age: number = 25;
```

### 2. **类型推断**

TypeScript 可以自动推断变量类型，即使不显式声明类型，TypeScript 也会根据变量的赋值内容来推断类型，从而在大多数情况下减少类型注解的书写量。

```ts
let name = "Alice"; // 推断为 string
```

### 3. **接口 (Interfaces)**

TypeScript 提供了接口，允许定义复杂的对象结构。接口可以定义属性和方法，还可以通过 `implements` 关键字实现接口，或者通过 `extends` 进行扩展，便于定义复杂的数据类型。

```ts
interface Person {
  name: string;
  age: number;
  greet(): void;
}

class Student implements Person {
  constructor(public name: string, public age: number) {}

  greet() {
    console.log(`Hello, my name is ${this.name}`);
  }
}
```

### 4. **类型别名 (Type Aliases)**

类型别名 (`type`) 可以为复杂的类型定义简短的别名，便于代码复用。

```ts
type StringOrNumber = string | number;
let value: StringOrNumber = 42;
```

### 5. **枚举 (Enums)**

TypeScript 引入了 `enum` 类型，用于定义一组命名的常量，提高代码的可读性。枚举在 JavaScript 中没有直接的对应。

```ts
enum Direction {
  Up,
  Down,
  Left,
  Right,
}
let dir: Direction = Direction.Up;
```

### 6. **元组 (Tuples)**

元组允许定义具有固定数量和类型的数组。它适用于需要固定数据结构的场景，比如坐标或 RGB 颜色值。

```ts
let point: [number, number] = [10, 20];
```

### 7. **访问控制修饰符 (Access Modifiers)**

TypeScript 在类中提供了 `public`、`private` 和 `protected` 修饰符，允许控制属性或方法的可见性，支持更好的封装。

```ts
class Person {
  private name: string;
  protected age: number;
  public constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
  }
}
```

### 8. **抽象类 (Abstract Classes)**

TypeScript 支持抽象类，抽象类不能直接实例化，需要由子类实现。抽象类适用于定义通用行为和抽象方法的类层次结构。

```ts
abstract class Animal {
  abstract makeSound(): void;
}

class Dog extends Animal {
  makeSound() {
    console.log("Woof!");
  }
}
```

### 9. **泛型 (Generics)**

TypeScript 支持泛型，允许在类、接口和函数中使用参数化类型，使得代码可以适应不同的类型需求，同时保持类型安全。

```ts
function identity<T>(value: T): T {
  return value;
}

let num = identity<number>(42);
```

### 10. **模块和命名空间**

TypeScript 提供了基于 ES6 的模块系统，使用 `import` 和 `export` 导入和导出模块。此外，TypeScript 还支持命名空间（Namespace），用于组织代码和避免命名冲突。

```ts
// math.ts
export function add(a: number, b: number): number {
  return a + b;
}

// main.ts
import { add } from "./math";
console.log(add(2, 3));
```

### 11. **类型守卫 (Type Guards)**

TypeScript 提供了类型守卫，可以在代码中检查变量类型，帮助编译器推断更加具体的类型。这对于联合类型尤为重要。

```ts
function printId(id: string | number) {
  if (typeof id === "string") {
    console.log(id.toUpperCase());
  } else {
    console.log(id.toFixed(2));
  }
}
```

### 12. **可选链和空值合并运算符**

TypeScript 增加了 JavaScript 的可选链 (`?.`) 和空值合并运算符 (`??`)，简化了代码中对可能为 `null` 或 `undefined` 值的处理。

```ts
let user = { name: "Alice", address: { city: "Wonderland" } };
console.log(user?.address?.city); // 如果 address 存在则输出 city，否则返回 undefined

let value = null;
console.log(value ?? "default"); // 如果 value 为 null 或 undefined，则返回 "default"
```

### 13. **类型兼容性和工具类型**

TypeScript 提供了一些工具类型，如 `Partial`、`Pick`、`Readonly`、`Record` 等，这些类型可以帮助生成新的类型，简化类型定义。

```ts
interface Todo {
  title: string;
  description: string;
}

let partialTodo: Partial<Todo> = { title: "Learn TypeScript" }; // 可选属性
```

### 14. **编译期错误检查**

TypeScript 提供的编译期错误检查可以捕获 JavaScript 中不易发现的错误，如拼写错误、类型不匹配等，帮助提升代码质量。

### 15. **ES 新特性支持**

TypeScript 提前支持了一些还未在所有环境中普及的 ES 特性，如装饰器（Decorators）、异步迭代器等，且能够将其编译成兼容 JavaScript 版本。

通过这些特性，TypeScript 提供了更安全、更结构化的代码能力，在大型项目和多人协作中尤其具有优势。



## typescript基本语法

TypeScript 程序由以下几个部分组成：

- 模块
- 函数
- 变量
- 语句和表达式
- 注释

我们可以使用以下 TypeScript 程序来输出 "Hello World" ：

```ts
const hello : string = "Hello World!"
console.log(hello)
```

以上代码首先通过 **tsc** 命令编译：

```sh
tsc Runoob.ts
```

得到如下 js 代码：

```js
var hello = "Hello World!";
console.log(hello);
```

最后我们使用 node 命令来执行该 js 代码。

```shell
$ node Runoob.js
Hello World
```

整个流程如下图所示：

![img](../../assets/图片/ts-2020-11-26-3.png)

### 空白和换行

TypeScript 会忽略程序中出现的空格、制表符和换行符。

空格、制表符通常用来缩进代码，使代码易于阅读和理解。

### TypeScript 区分大小写

TypeScript 区分大写和小写字符。

### 分号是可选的

每行指令都是一段语句，你可以使用分号或不使用， 分号在 TypeScript 中是可选的，建议使用。

以下代码都是合法的：

```
console.log("Runoob")
console.log("Google");
```

如果语句写在同一行则一定需要使用分号来分隔，否则会报错，如：

```
console.log("Runoob");console.log("Google");
```

### TypeScript 注释

注释是一个良好的习惯，虽然很多程序员讨厌注释，但还是建议你在每段代码写上文字说明。

注释可以提高程序的可读性。

注释可以包含有关程序一些信息，如代码的作者，有关函数的说明等。

编译器会忽略注释。

### TypeScript 支持两种类型的注释

- **单行注释 ( // )** − 在 // 后面的文字都是注释内容。
- **多行注释 (/\* \*/)** − 这种注释可以跨越多行。

注释实例：

```ts
// 这是一个单行注释
 
/* 
 这是一个多行注释 
 这是一个多行注释 
 这是一个多行注释 
*/
```

### TypeScript 与面向对象

面向对象是一种对现实世界理解和抽象的方法。TypeScript 是一种面向对象的编程语言。

> 和C#差不多啦



## Typescript基本结构

### 1. 声明部分（Declarations）

**类型声明：**TypeScript 是一种静态类型的语言，可以通过类型声明来定义变量、函数、类等的类型。类型声明可以帮助代码更具可维护性和可读性。

```ts
let name: string = "Alice";
let age: number = 30;
```

**接口声明：**用于定义对象的结构，包括对象的属性和方法。

```ts
interface Person {
    name: string;
    age: number;
}
```

### 2. 变量声明（Variable Declarations）

在 TypeScript 中，可以使用 let, const, 和 var 来声明变量。推荐使用 let 和 const，var 用法不再推荐。

```ts
let age: number = 25;
const pi: number = 3.14;
```

>**`var`**
>
>- **函数作用域**：在整个函数内都有效。
>- 如果在函数外声明，就是挂在 `window`（浏览器环境）上的全局变量。
>
>**`let` 和 `const`**
>
>- **块级作用域**：只在 `{}` 内有效，比如 `if`、`for` 里。
>- 不会被挂到 `window` 上。

### 3. 函数声明（Function Declarations）

函数声明：TypeScript 允许声明带有类型注解的函数，包括参数类型和返回值类型。

```ts
function greet(name: string): string {
    return "Hello, " + name;
}
```

**箭头函数：**TypeScript 同样支持 ES6 的箭头函数，使用简洁的语法来声明函数。

```ts
const greet = (name: string): string => "Hello, " + name;
```

### 4. 类声明（Class Declarations）

TypeScript 提供对面向对象编程的支持，允许定义类和类的方法、属性。

```ts
class Person {
    name: string;
    age: number;
    
    constructor(name: string, age: number) {
    this.name = name;
    this.age = age;
    }
    
    greet() {
    return `Hello, my name is ${this.name}`;
    }
}
```

### 5. 接口与类型别名（Interfaces & Type Aliases）

接口（Interface）：用于描述对象的形状，接口可以继承和扩展。

```ts
interface Animal {
    name: string;
    sound: string;
    makeSound(): void;
}
```

**类型别名（Type Alias）：**允许为对象类型、联合类型、交叉类型等定义别名。

```ts
type ID = string | number; //就是这个id可以是string或者number，两者都可以
```

>同时也有联合数组：
>
>```ts
>var arr:number[]|string[]; 
>var i:number; 
>arr = [1,2,4] 
>console.log("**数字数组**")  
> 
>for(i = 0;i<arr.length;i++) { 
>   console.log(arr[i]) 
>}  
> 
>arr = ["Runoob","Google","Taobao"] 
>console.log("**字符串数组**")  
> 
>for(i = 0;i<arr.length;i++) { 
>   console.log(arr[i]) 
>} 
>```

### 6. 模块和导入导出（Modules & Imports/Exports）

TypeScript 支持模块化编程，可以使用 import 和 export 来组织代码。

```ts
export class Person {
    constructor(public name: string) {}
}
```

```ts
import { Person } from './person';
```

### 7. 类型断言（Type Assertions）

在某些情况下，TypeScript 无法推断出一个变量的准确类型，开发者可以使用类型断言来强制指定类型。

```ts
let value: any = "hello";
let strLength: number = (value as string).length;
```

### 8. 泛型（Generics）

泛型允许在定义函数、接口或类时不指定具体类型，而是使用占位符，让用户在使用时传入具体类型。泛型能够增加代码的复用性和类型安全性。

```ts
function identity<T>(arg: T): T {
    return arg;
}
```

### 9. 注释

同C语言。

### 10. 类型推断（Type Inference）

TypeScript 在某些情况下会自动推断变量的类型。例如，在声明变量并赋值时，TypeScript 会推断出该变量的类型。

```ts
let num = 10;  // TypeScript 推断 num 为 number 类型
```

### 11. 类型守卫（Type Guards）

TypeScript 提供了类型守卫（如 typeof 和 instanceof），用于在运行时缩小变量的类型范围。

```ts
function isString(value: any): value is string {
    return typeof value === 'string';
}
```

### 12. 异步编程（Asynchronous Programming）

TypeScript 完全支持异步编程，可以使用 async/await 语法来处理异步操作。

```ts
async function fetchData(): Promise<string> {
    const response = await fetch("https://example.com");
    const data = await response.text();
    return data;
}
```

### 13. 错误处理（Error Handling）

TypeScript 允许使用 try/catch 块进行错误处理，还可以使用类型来描述错误的类型。

```ts
try {
    throw new Error("Something went wrong");
} catch (error) {
    if (error instanceof Error) {
        console.error(error.message);
    }
}
```



## typescript数据类型

基础类型可以开发者更准确地描述数据的结构和意图。

TypeScript 包含的数据类型如下表:

| 类型        | 描述                             | 示例                                                    |
| :---------- | :------------------------------- | :------------------------------------------------------ |
| `string`    | 表示文本数据                     | `let name: string = "Alice";`                           |
| `number`    | 表示数字，包括整数和浮点数       | `let age: number = 30;`                                 |
| `boolean`   | 表示布尔值 `true` 或 `false`     | `let isDone: boolean = true;`                           |
| `array`     | 表示相同类型的元素数组           | `let list: number[] = [1, 2, 3];`                       |
| `tuple`     | 表示已知类型和长度的数组         | `let person: [string, number] = ["Alice", 30];`         |
| `enum`      | 定义一组命名常量                 | `enum Color { Red, Green, Blue };`                      |
| `any`       | 任意类型，不进行类型检查         | `let value: any = 42;`                                  |
| `void`      | 无返回值（常用于函数）           | `function log(): void {}`                               |
| `null`      | 表示空值                         | `let empty: null = null;`                               |
| `undefined` | 表示未定义                       | `let undef: undefined = undefined;`                     |
| `never`     | 表示不会有返回值                 | `function error(): never { throw new Error("error"); }` |
| `object`    | 表示非原始类型                   | `let obj: object = { name: "Alice" };`                  |
| `union`     | 联合类型，表示可以是多种类型之一 | `let id: string                                         |
| `unknown`   | 不确定类型，需类型检查后再使用   | `let value: unknown = "Hello";`                         |

**注意：**TypeScript 和 JavaScript 没有整数类型。

### 1、string 字符串

表示文本数据，只能存储字符串，通常用于描述文字信息。

```ts
let message: string = "Hello, TypeScript!";
```

**模板字符串：**TypeScript 支持 **模板字符串**，用反引号 **`**（记住不是单引号 **'**）来定义，允许在字符串中插入变量或表达式，非常适合多行文本和拼接变量。

```ts
let name: string = "Alice";
let greeting: string = `Hello, ${name}! Welcome to TypeScript.`;
console.log(greeting); // 输出：Hello, Alice! Welcome to TypeScript.
```

### 2、number 数字

TypeScript 使用 number 表示所有数字，包括整数和浮点数。

```ts
let age: number = 25;
let temperature: number = 36.5;
```

### 3、boolean 布尔值

表示逻辑值 true 或 false，用于条件判断。

```ts
let isCompleted: boolean = false;
```

### 4、array 数组

可以表示一组相同类型的元素。可以使用 type[] 或 Array<type> 两种方式表示。

```ts
let numbers: number[] = [1, 2, 3];
let names: Array<string> = ["Alice", "Bob"];
```

### 5、tuple 元组

表示已知数量和类型的数组。每个元素可以是不同的类型，适合表示固定结构的数据。

```ts
let person: [string, number] = ["Alice", 25];
```

### 6、enum 枚举

用来定义一组命名常量。默认情况下枚举的值从 0 开始递增。

```ts
enum Color {
  Red,
  Green,
  Blue,
}
let favoriteColor: Color = Color.Green;
```

### 7、any 类型

以表示任何类型。适合不确定数据类型的情况，但使用时需谨慎，因为 any 会绕过类型检查。

```ts
let randomValue: any = 42;
randomValue = "hello";
```

任意值是 TypeScript 针对编程时类型不明确的变量使用的一种数据类型，它常用于以下三种情况。

1、变量的值会动态改变时，比如来自用户的输入，任意值类型可以让这些变量跳过编译阶段的类型检查，示例代码如下：

```ts
let x: any = 1;    // 数字类型
x = 'I am who I am';    // 字符串类型
x = false;    // 布尔类型
```

改写现有代码时，任意值允许在编译时可选择地包含或移除类型检查，示例代码如下：

```ts
let x: any = 4;
x.ifItExists();    // 正确，ifItExists方法在运行时可能存在，但这里并不会检查
x.toFixed();    // 正确
```

定义存储各种类型数据的数组时，示例代码如下：

```ts
let arrayList: any[] = [1, false, 'fine'];
arrayList[1] = 100;
```

### 8、void 空类型

用于没有返回值的函数。声明变量时，类型 void 意味着只能赋值 null 或 undefined。

```ts
function logMessage(message: string): void {
  console.log(message);
}
```

### 9、null 和 undefined

null 和 undefined分别表示"空值"和"未定义"。在默认情况下，它们是所有类型的子类型，但可以通过设置 strictNullChecks 严格检查。

```ts
let empty: null = null;
let notAssigned: undefined = undefined;
```

**null**

在 JavaScript 中 null 表示 "什么都没有"。

null是一个只有一个值的特殊类型。表示一个空对象引用。

用 typeof 检测 null 返回是 object。

**undefined**

在 JavaScript 中, undefined 是一个没有设置值的变量。

typeof 一个没有值的变量会返回 undefined。

Null 和 Undefined 是其他任何类型（包括 void）的子类型，可以赋值给其它类型，如数字类型，此时，赋值后的类型会变成 null 或 undefined。而在TypeScript中启用严格的空校验（--strictNullChecks）特性，就可以使得null 和 undefined 只能被赋值给 void 或本身对应的类型，示例代码如下：

```ts
// 启用 --strictNullChecks
let x: number;
x = 1; // 编译正确
x = undefined;    // 编译错误
x = null;    // 编译错误
```

上面的例子中变量 x 只能是数字类型。如果一个类型可能出现 null 或 undefined， 可以用 | 来支持多种类型，示例代码如下：

```ts
// 启用 --strictNullChecks
let x: number | null | undefined;
x = 1; // 编译正确
x = undefined;    // 编译正确
x = null;    // 编译正确
```

### 10、never 类型

表示不会有返回值，通常用于抛出错误或进入无限循环的函数，表示该函数永远不会正常结束。

```ts
function throwError(message: string): never {
  throw new Error(message);
}
```

never 是其它类型（包括 null 和 undefined）的子类型，代表从不会出现的值。这意味着声明为 never 类型的变量只能被 never 类型所赋值，在函数中它通常表现为抛出异常或无法执行到终止点（例如无限循环），示例代码如下：

```ts
let x: never;
let y: number;

// 编译错误，数字类型不能转为 never 类型
x = 123;

// 运行正确，never 类型可以赋值给 never类型
x = (()=>{ throw new Error('exception')})();

// 运行正确，never 类型可以赋值给 数字类型
y = (()=>{ throw new Error('exception')})();

// 返回值为 never 的函数可以是抛出异常的情况
function error(message: string): never {
    throw new Error(message);
}

// 返回值为 never 的函数可以是无法被执行到的终止点的情况
function loop(): never {
    while (true) {}
}
```

### 11、object 对象类型

表示非原始类型的值，适用于复杂的对象结构。

```ts
let person: object = { name: "Alice", age: 30 };
```

### 12、联合类型 (Union)

表示一个变量可以是多种类型之一。通过 | 符号实现。

```ts
let id: string | number;
id = "123";
id = 456;
```

### 13、unknown 不确定的类型

与 any 类似，但更严格。必须经过类型检查后才能赋值给其他类型变量。

```ts
let value: unknown = "Hello";
if (typeof value === "string") {
  let message: string = value;
}
```

### 14、类型断言 (Type Assertions)

类型断言可以让开发者明确告诉编译器变量的类型，常用于无法推断的情况。可以使用 as 或尖括号语法。

```ts
let someValue: any = "this is a string";
let strLength: number = (someValue as string).length;
```

### 15、字面量类型

字面量类型可以让变量只能拥有特定的值，用于结合联合类型定义变量的特定状态。

```ts
let direction: "up" | "down" | "left" | "right";
direction = "up";
```

通过这些类型，TypeScript 提供了更强的类型安全性和代码检查能力，使开发者能够更清晰、准确地表达数据和意图，减少运行时错误。



## TypeScript 变量声明

变量是一种使用方便的占位符，用于引用计算机内存地址。我们可以把变量看做存储数据的容器。

TypeScript 变量的命名规则：

- 变量名称可以包含数字和字母。
- 除了下划线 **_** 和美元 **$** 符号外，不能包含其他特殊字符，包括空格。
- 变量名不能以数字开头。

变量使用前必须先声明，我们可以使用 var 来声明变量。我们可以使用以下四种方式来声明变量：

声明变量的类型及初始值：

```ts
var [变量名] : [类型] = 值;
```

例如：

```ts
var uname:string = "Runoob";
```

声明变量的类型，但没有初始值，变量值会设置为 undefined：

```ts
var [变量名] : [类型];
```

例如：

```ts
var uname:string;
```

声明变量并初始值，但不设置类型，该变量可以是任意类型：

```
var [变量名] = 值;
```

例如：

```ts
var uname = "Runoob";
```

声明变量没有设置类型和初始值，类型可以是任意类型，默认初始值为 undefined：

```ts
var [变量名];
```

例如：

```ts
var uname;
```



## 运算符

typescript运算符和C语言一样。

## 控制

> 这里`for`循环和`while`循环同C语言



## TypeScript 函数

函数是一组一起执行一个任务的语句。

您可以把代码划分到不同的函数中。如何划分代码到不同的函数中是由您来决定的，但在逻辑上，划分通常是根据每个函数执行一个特定的任务来进行的。

函数声明告诉编译器函数的名称、返回类型和参数。函数定义提供了函数的实际主体。

### 1 函数定义

函数就是包裹在花括号中的代码块，前面使用了关键词 function：

语法格式如下所示：

```ts
function function_name()
{
    // 执行代码
}
```

### 2 带参数函数

在调用函数时，您可以向其传递值，这些值被称为参数。

这些参数可以在函数中使用。

您可以向函数发送多个参数，每个参数使用逗号 **,** 分隔：

```ts
function func_name( param1 [:datatype], param2 [:datatype]) {   
}
```

- param1、param2 为参数名。
- datatype 为参数类型。

```ts
function add(x: number, y: number): number {
    return x + y;
}
console.log(add(1,2))
```

### 3 可选参数

在 TypeScript 函数里，如果我们定义了参数，则我们必须传入这些参数，除非将这些参数设置为可选，可选参数使用问号标识 ？。

```ts
function buildName(firstName: string, lastName?: string) {
    if (lastName)
        return firstName + " " + lastName;
    else
        return firstName;
}
 
let result1 = buildName("Bob");  // 正确
let result2 = buildName("Bob", "Adams", "Sr.");  // 错误，参数太多了
let result3 = buildName("Bob", "Adams");  // 正确
```

### 4 默认参数

我们也可以设置参数的默认值，这样在调用函数的时候，如果不传入该参数的值，则使用默认参数，语法格式为：

```ts
function function_name(param1[:type],param2[:type] = default_value) { 
}
```

注意：参数不能同时设置为可选和默认。

```ts
function calculate_discount(price:number,rate:number = 0.50) { 
    var discount = price * rate; 
    console.log("计算结果: ",discount); 
} 
calculate_discount(1000) 
calculate_discount(1000,0.30)
```

### 5 剩余参数

有一种情况，我们不知道要向函数传入多少个参数，这时候我们就可以使用剩余参数来定义。

剩余参数语法允许我们将一个不确定数量的参数作为一个数组传入。

```ts
function buildName(firstName: string, ...restOfName: string[]) {
    return firstName + " " + restOfName.join(" ");
}
  
let employeeName = buildName("Joseph", "Samuel", "Lucas", "MacKinzie");
```

```ts
function addNumbers(...nums:number[]) {  
    var i;   
    var sum:number = 0; 
    
    for(i = 0;i<nums.length;i++) { 
       sum = sum + nums[i]; 
    } 
    console.log("和为：",sum) 
 } 
 addNumbers(1,2,3) 
 addNumbers(10,10,10,10,10)
```

### 6 匿名函数

匿名函数是一个没有函数名的函数。

匿名函数在程序运行时动态声明，除了没有函数名外，其他的与标准函数一样。

我们可以将匿名函数赋值给一个变量，这种表达式就成为函数表达式。

语法格式如下：

```ts
var res = function( [arguments] ) { ... }
```

```ts
var msg = function() { 
    return "hello world";  
} 
console.log(msg())
```

### 7 匿名函数自调用

匿名函数自调用在函数后使用 () 即可：

```ts
(function () { 
    var x = "Hello!!";   
    console.log(x)     
 })()
```

输出 `Hello!!`

### 8 构造函数

TypeScript 也支持使用 JavaScript 内置的构造函数 Function() 来定义函数：

语法格式如下：

```ts
var res = new Function ([arg1[, arg2[, ...argN]],] functionBody)
```

参数说明：

- **arg1, arg2, ... argN**：参数列表。
- **functionBody**：一个含有包括函数定义的 JavaScript 语句的字符串。

```ts
var myFunction = new Function("a", "b", "return a * b"); 
var x = myFunction(4, 3); 
console.log(x);
```

### 9 递归函数

同C，不再赘述

### 10 Lambda 函数

Lambda 函数也称之为箭头函数。箭头函数表达式的语法比函数表达式更短。

函数只有一行语句：

```ts
( [param1, param2,…param n] )=>statement;
```

```ts
var foo = (x:number)=> {    
    x = 10 + x 
    console.log(x)  
} 
foo(100)
```

### 11 函数重载

重载是方法名字相同，而参数不同，返回类型可以相同也可以不同。

每个重载的方法（或者构造函数）都必须有一个独一无二的参数类型列表。

参数类型不同：

```ts
function disp(string):void; 
function disp(number):void;
```

参数数量不同：

```ts
function disp(n1:number):void; 
function disp(x:number,y:number):void;
```

参数类型顺序不同：

```ts
function disp(n1:number,s1:string):void; 
function disp(s:string,n:number):void;
```

如果参数类型不同，则参数类型应设置为 **any**。参数数量不同你可以将不同的参数设置为可选。

> 具体可参照C#方法重载



## TypeScript Array(数组)

常见写法：

```ts
var array_name[:datatype] = [val1,val2…valn]
```

### 1 Array 对象

我们也可以使用 Array 对象创建数组。

Array 对象的构造函数接受以下两种值：

- 表示数组大小的数值。
- 初始化的数组列表，元素使用逗号分隔值。

```ts
var arr_names:number[] = new Array(4)  
 
for(var i = 0; i<arr_names.length; i++) { 
        arr_names[i] = i * 2 
        console.log(arr_names[i]) 
}
```

### 2 数组解构

我们也可以把数组元素赋值给变量，如下所示：

```ts
var arr:number[] = [12,13] 
var[x,y] = arr // 将数组的两个元素赋值给变量 x 和 y
console.log(x) 
console.log(y)
```

### 3 数组迭代

我们可以使用 for 语句来循环输出数组的各个元素：

```ts
var j:any; 
var nums:number[] = [1001,1002,1003,1004] 
 
for(j in nums) { 
    console.log(nums[j]) 
}
```

> 一些常见的数组方法，如`arr.sort()`请具体查看文档



## TypeScript Map 对象

Map 对象保存键值对，并且能够记住键的原始插入顺序。

任何值(对象或者原始值) 都可以作为一个键或一个值。

### 1 创建 Map

TypeScript 使用 Map 类型和 new 关键字来创建 Map：

```ts
let myMap = new Map();
```

初始化 Map，可以以数组的格式来传入键值对：

```ts
let myMap = new Map([
        ["key1", "value1"],
        ["key2", "value2"]
    ]); 
```

Map 相关的函数与属性：

- **map.clear()** – 移除 Map 对象的所有键/值对 。
- **map.set()** – 设置键值对，返回该 Map 对象。
- **map.get()** – 返回键对应的值，如果不存在，则返回 undefined。
- **map.has()** – 返回一个布尔值，用于判断 Map 中是否包含键对应的值。
- **map.delete()** – 删除 Map 中的元素，删除成功返回 true，失败返回 false。
- **map.size** – 返回 Map 对象键/值对的数量。
- **map.keys()** - 返回一个 Iterator 对象， 包含了 Map 对象中每个元素的键 。
- **map.values()** – 返回一个新的Iterator对象，包含了Map对象中每个元素的值 。
- **map.entries()** – 返回一个包含 Map 中所有键值对的迭代器 。

### 2 常用函数

**set(key: K, value: V): this** - 向 Map 中添加或更新键值对。

```ts
map.set('key1', 'value1');
```

**get(key: K): V | undefined** - 根据键获取值，如果键不存在则返回 undefined。

```ts
const value = map.get('key1');
```

**has(key: K): boolean** - 检查 Map 中是否存在指定的键。

```ts
const exists = map.has('key1');
```

**delete(key: K): boolean** - 删除指定键的键值对，成功删除返回 true，否则返回 false。

```ts
const removed = map.delete('key1');
```

**clear(): void** - 清空 Map 中的所有键值对。

```ts
map.clear();
```

**size: number** - 返回 Map 中键值对的数量。

```ts
const size = map.size;
```

### 3 迭代方法

keys(): IterableIterator\<K> - 返回一个包含 Map 中所有键的迭代器。

```ts
for (const key of map.keys()) {
  console.log(key);
}
```

**values(): IterableIterator\<V>** - 返回一个包含 Map 中所有值的迭代器。

```ts
for (const value of map.values()) {
  console.log(value);
}
```

**entries(): IterableIterator<[K, V]>** - 返回一个包含 Map 中所有键值对的迭代器，每个元素是一个 [key, value] 数组。

```ts
for (const [key, value] of map.entries()) {
  console.log(key, value);
}
```

**forEach(callbackfn: (value: V, key: K, map: Map<K, V>) => void, thisArg?: any): void** - 对 Map 中的每个键值对执行一次提供的回调函数。

```ts
map.forEach((value, key) => {
  console.log(key, value);
});
```

实例：

```ts
let nameSiteMapping = new Map();
 
// 设置 Map 对象
nameSiteMapping.set("Google", 1);
nameSiteMapping.set("Runoob", 2);
nameSiteMapping.set("Taobao", 3);
 
// 获取键对应的值
console.log(nameSiteMapping.get("Runoob"));     // 2
 
// 判断 Map 中是否包含键对应的值
console.log(nameSiteMapping.has("Taobao"));       // true
console.log(nameSiteMapping.has("Zhihu"));        // false
 
// 返回 Map 对象键/值对的数量
console.log(nameSiteMapping.size);                // 3
 
// 删除 Runoob
console.log(nameSiteMapping.delete("Runoob"));    // true
console.log(nameSiteMapping);
// 移除 Map 对象的所有键/值对
nameSiteMapping.clear();             // 清除 Map
console.log(nameSiteMapping);
```



## TypeScript 元组

我们知道数组中元素的数据类型都一般是相同的（any[] 类型的数组可以不同），如果存储的元素数据类型不同，则需要使用元组。

TypeScript 中的元组（Tuple）是一种特殊类型的数组，它允许在数组中存储不同类型的元素，与普通数组不同，元组中的每个元素都有明确的类型和位置。元组可以在很多场景下用于表示固定长度、且各元素类型已知的数据结构。

创建元组的语法格式如下：

```ts
let tuple: [类型1, 类型2, 类型3, ...];
```

声明一个元组并初始化：

```ts
let mytuple: [number, string];
mytuple = [42,"Runoob"];
```

在上面的例子中，mytuple 是一个元组，它包含一个 number 类型和一个 string 类型的元素。

### 1 访问元组

元组中元素使用索引来访问，第一个元素的索引值为 0，第二个为 1，以此类推第 n 个为 n-1，语法格式如下:

```ts
tuple_name[index]
```

以下实例定义了元组，包含了数字和字符串两种类型的元素：

```ts
let mytuple: [number, string, boolean] = [42, "Runoob", true];
 
// 访问元组中的元素
let num = mytuple[0]; // 访问第一个元素，值为 42，类型为 number
let str = mytuple[1]; // 访问第二个元素，值为 "Runoob"，类型为 string
let bool = mytuple[2]; // 访问第三个元素，值为 true，类型为 boolean
 
console.log(num);  // 输出: 42
console.log(str);  // 输出: Runoob
console.log(bool); // 输出: true
```

### 2 元组运算

我们可以使用以下两个函数向元组添加新元素或者删除元素：

- push() 向元组添加元素，添加在最后面。
- pop() 从元组中移除元素（最后一个），并返回移除的元素。

push 方法可以向元组的末尾添加一个元素，类型必须符合元组定义中的类型约束。如果超出元组的类型约束，TypeScript 会报错。

### 3 解构元组

我们也可以把元组元素赋值给变量，如下所示：

```ts
let a: [number, string, boolean] = [42, "Hello", true];// 创建一个元组
 
var [b,c] = a 
console.log( b )    
console.log( c )
```

> 更多操作请参照文档。

## TypeScript 接口

接口是一系列抽象方法的声明，是一些方法特征的集合，这些方法都应该是抽象的，需要由具体的类去实现，然后第三方就可以通过这组抽象方法调用，让具体的类执行具体的方法。

TypeScript 接口定义如下：

```ts
interface interface_name { 
}
```

以下实例中，我们定义了一个接口 IPerson，接着定义了一个变量 customer，它的类型是 IPerson。

customer 实现了接口 IPerson 的属性和方法。

```ts
interface IPerson { 
    firstName:string, 
    lastName:string, 
    sayHi: ()=>string 
} 
 
var customer:IPerson = { 
    firstName:"Tom",
    lastName:"Hanks", 
    sayHi: ():string =>{return "Hi there"} 
} 
 
console.log("Customer 对象 ") 
console.log(customer.firstName) 
console.log(customer.lastName) 
console.log(customer.sayHi())  
 
var employee:IPerson = { 
    firstName:"Jim",
    lastName:"Blakes", 
    sayHi: ():string =>{return "Hello!!!"} 
} 
 
console.log("Employee  对象 ") 
console.log(employee.firstName) 
console.log(employee.lastName)
```

### 1 联合类型和接口

以下实例演示了如何在接口中使用联合类型：

```ts
interface RunOptions { 
    program:string; 
    commandline:string[]|string|(()=>string); 
} 
 
// commandline 是字符串
var options:RunOptions = {program:"test1",commandline:"Hello"}; 
console.log(options.commandline)  
 
// commandline 是字符串数组
options = {program:"test1",commandline:["Hello","World"]}; 
console.log(options.commandline[0]); 
console.log(options.commandline[1]);  
 
// commandline 是一个函数表达式
options = {program:"test1",commandline:()=>{return "**Hello World**";}}; 
 
var fn:any = options.commandline; 
console.log(fn());
```

### 2 接口和数组

接口中我们可以将数组的索引值和元素设置为不同类型，索引值可以是数字或字符串。

设置元素为字符串类型：

```ts
interface namelist { 
   [index:number]:string 
} 
 
// 类型一致，正确
var list2:namelist = ["Google","Runoob","Taobao"]
// 错误元素 1 不是 string 类型
// var list2:namelist = ["Runoob",1,"Taobao"]
```

### 3 接口继承

接口继承就是说接口可以通过其他接口来扩展自己。

Typescript 允许接口继承多个接口。

继承使用关键字 **extends**。

单接口继承语法格式：

```ts
Child_interface_name extends super_interface_name
```

多接口继承语法格式：

```ts
Child_interface_name extends super_interface1_name, super_interface2_name,…,super_interfaceN_name
```

继承的各个接口使用逗号 **,** 分隔。

### 4 多继承实例

```ts
interface IParent1 { 
    v1:number 
} 
 
interface IParent2 { 
    v2:number 
} 
 
interface Child extends IParent1, IParent2 { } 
var Iobj:Child = { v1:12, v2:23} 
console.log("value 1: "+Iobj.v1+" value 2: "+Iobj.v2)
```

## TypeScript 类

TypeScript 是面向对象的 JavaScript。类描述了所创建的对象共同的属性和方法。

TypeScript 支持面向对象的所有特性，比如 类、接口等。TypeScript 类定义方式如下：

```ts
class class_name { 
    // 类作用域
}
```

定义类的关键字为 class，后面紧跟类名，类可以包含以下几个模块（类的数据成员）：

- **字段** − 字段是类里面声明的变量。字段表示对象的有关数据。
- **构造函数** − 类实例化时调用，可以为类的对象分配内存。
- **方法** − 方法为对象要执行的操作。

### 1 创建类的数据成员

以下实例我们声明了类 Car，包含字段为 engine，构造函数在类实例化后初始化字段 engine。

this 关键字表示当前类实例化的对象。注意构造函数的参数名与字段名相同，this.engine 表示类的字段。

此外我们也在类中定义了一个方法 disp()。

```ts
class Car { 
    // 字段 
    engine:string; 
 
    // 构造函数 
    constructor(engine:string) { 
        this.engine = engine 
    }  
 
    // 方法 
    disp():void { 
        console.log("发动机为 :   "+this.engine) 
    } 
}
```

### 2 创建实例化对象

我们使用 new 关键字来实例化类的对象，语法格式如下：

```ts
var object_name = new class_name([ arguments ])
```

类实例化时会调用构造函数，例如：

```ts
var obj = new Car("Engine 1")
```

类中的字段属性和方法可以使用 **.** 号来访问：

```ts
// 访问属性
obj.field_name 

// 访问方法
obj.function_name()
```

完整实例：

```ts
class Car { 
   // 字段
   engine:string; 
   
   // 构造函数
   constructor(engine:string) { 
      this.engine = engine 
   }  
   
   // 方法
   disp():void { 
      console.log("函数中显示发动机型号  :   "+this.engine) 
   } 
} 
 
// 创建一个对象
var obj = new Car("XXSY1")
 
// 访问字段
console.log("读取发动机型号 :  "+obj.engine)  
 
// 访问方法
obj.disp()
```

### 3 类的继承

TypeScript 支持继承类，即我们可以在创建类的时候继承一个已存在的类，这个已存在的类称为父类，继承它的类称为子类。

类继承使用关键字 **extends**，子类除了不能继承父类的私有成员(方法和属性)和构造函数，其他的都可以继承。

TypeScript 一次只能继承一个类，不支持继承多个类，但 TypeScript 支持多重继承（A 继承 B，B 继承 C）。

语法格式如下：

```
class child_class_name extends parent_class_name
```

```ts
class Shape { 
   Area:number 
   
   constructor(a:number) { 
      this.Area = a 
   } 
} 
 
class Circle extends Shape { 
   disp():void { 
      console.log("圆的面积:  "+this.Area) 
   } 
}
  
var obj = new Circle(223); 
obj.disp()
```

需要注意的是子类只能继承一个父类，TypeScript 不支持继承多个类，但支持多重继承，如下实例：

```ts
class Root { 
   str:string; 
} 
 
class Child extends Root {} 
class Leaf extends Child {} // 多重继承，继承了 Child 和 Root 类
 
var obj = new Leaf(); 
obj.str ="hello" 
console.log(obj.str)
```

### 4 继承类的方法重写

类继承后，子类可以对父类的方法重新定义，这个过程称之为方法的重写。

其中 ==super== 关键字是对父类的直接引用，该关键字可以引用父类的属性和方法。

```ts
class PrinterClass { 
   doPrint():void {
      console.log("父类的 doPrint() 方法。") 
   } 
} 
 
class StringPrinter extends PrinterClass { 
   doPrint():void { 
      super.doPrint() // 调用父类的函数
      console.log("子类的 doPrint()方法。")
   } 
}
```

### 5 static 关键字

static 关键字用于定义类的数据成员（属性和方法）为静态的，静态成员可以直接通过类名调用。

```ts
class StaticMem {  
   static num:number; 
   
   static disp():void { 
      console.log("num 值为 "+ StaticMem.num) 
   } 
} 
 
StaticMem.num = 12     // 初始化静态变量
StaticMem.disp()       // 调用静态方法
```

### 6 访问控制修饰符

TypeScript 中，可以使用访问控制符来保护对类、变量、方法和构造方法的访问。TypeScript 支持 3 种不同的访问权限。

- **public（默认）** : 公有，可以在任何地方被访问。
- **protected** : 受保护，可以被其自身以及其子类访问。
- **private** : 私有，只能被其定义所在的类访问。

以下实例定义了两个变量 str1 和 str2，str1 为 public，str2 为 private，实例化后可以访问 str1，如果要访问 str2 则会编译错误。

```ts
class Encapsulate { 
   str1:string = "hello" 
   private str2:string = "world" 
}
 
var obj = new Encapsulate() 
console.log(obj.str1)     // 可访问 
console.log(obj.str2)   // 编译错误， str2 是私有的
```

### 7 类和接口

类可以实现接口，使用关键字 implements，并将 interest 字段作为类的属性使用。

以下实例中 AgriLoan 类实现了 ILoan 接口：

```ts
interface ILoan { 
   interest:number 
} 
 
class AgriLoan implements ILoan { 
   interest:number 
   rebate:number 
   
   constructor(interest:number,rebate:number) { 
      this.interest = interest 
      this.rebate = rebate 
   } 
} 
 
var obj = new AgriLoan(10,1) 
console.log("利润为 : "+obj.interest+"，抽成为 : "+obj.rebate )
```

## TypeScript 对象

对象是包含一组键值对的实例。 值可以是标量、函数、数组、对象等，如下实例：

```ts
var object_name = { 
    key1: "value1", // 标量
    key2: "value",  
    key3: function() {
        // 函数
    }, 
    key4:["content1", "content2"] //集合
}
```

以上对象包含了标量，函数，集合(数组或元组)。

一个实例：

```ts
var sites = { 
   site1:"Runoob", 
   site2:"Google" 
}; 
// 访问对象的值
console.log(sites.site1) 
console.log(sites.site2)
```

>==好像不一样？==
>
>###### 1. C# 里的对象
>
>- **类 class** 是蓝图（模板），对象是通过 `new` 关键字实例化出来的：
>
>  ```c#
>  class Person {
>      public string Name { get; set; }
>      public void SayHi() {
>          Console.WriteLine($"Hi, I'm {Name}");
>      }
>  }
>  
>  var p = new Person { Name = "Tom" };
>  p.SayHi(); // Hi, I'm Tom
>  ```
>
>- 特点：
>
>  - **强类型**：类型在编译时就固定。
>  - **必须有类（class/struct）定义**，才能产生对象。
>  - **对象就是类的实例**。
>
>###### 2. JS/TS 里的对象
>
>在 **JavaScript/TypeScript** 中，"对象（object）" 是一种更灵活的数据结构，类似 **键值对（key-value map）**。
> 你看到的写法：
>
>```ts
>var obj = {
>    key1: "value1",   // 字符串
>    key2: 123,        // 数字
>    key3: function() {
>        console.log("hello");
>    },
>    key4: ["a", "b"]  // 数组
>};
>```
>
>- 它不是通过 `class` 产生的，而是 **字面量（object literal）** 直接写出来的。
>- 这种“对象”可以看作是 **灵活的数据包**，里面随便塞各种属性。
>- 在 TS 中你可以给它加类型约束
>
>###### 3. 衔接
>
>其实 **TS 里也有 class**，可以写得像 C#：
>
>```ts
>class Person {
>    name: string;
>    constructor(name: string) {
>        this.name = name;
>    }
>    sayHi() {
>        console.log(`Hi, I'm ${this.name}`);
>    }
>}
>
>let p = new Person("Tom");
>p.sayHi();
>```
>
>这样和 C# 就很像了。
> 但如果只是写配置、数据，JS/TS 社区更喜欢用对象字面量 `{}`，因为更简单。

### 1 对象的方法

>js是与C#是类似的。可以在对象中随时定义一个完整的方法。但是对于ts：

假如我们在 JavaScript 定义了一个对象：

```ts
var sites = { 
   site1:"Runoob", 
   site2:"Google" 
};
```

这时如果我们想在对象中添加方法，可以做以下修改：

```ts
sites.sayHello = function(){ return "hello";}
```

如果在 TypeScript 中使用以上方式则会出现编译错误，因为Typescript 中的对象必须是特定类型的实例。

```ts
var sites = {
    site1: "Runoob",
    site2: "Google",
    sayHello: function () { } // 类型模板
};
sites.sayHello = function () {
    console.log("hello " + sites.site1);
};
sites.sayHello();
```

这样需要在对象外定义方法。

### 2 类作为参数

此外对象也可以作为一个参数传递给函数，如下实例：

```ts
var sites = { 
    site1:"Runoob", 
    site2:"Google",
}; 
var invokesites = function(obj: { site1:string, site2 :string }) { 
    console.log("site1 :"+obj.site1) 
    console.log("site2 :"+obj.site2) 
} 
invokesites(sites)
```

### 3 鸭子类型(Duck Typing)

鸭子类型（英语：duck typing）是动态类型的一种风格，是多态(polymorphism)的一种形式。

在这种风格中，一个对象有效的语义，不是由继承自特定的类或实现特定的接口，而是由"当前方法和属性的集合"决定。

> 可以这样表述：
>
> "当看到一只鸟走起来像鸭子、游泳起来像鸭子、叫起来也像鸭子，那么这只鸟就可以被称为鸭子。"

在鸭子类型中，关注点在于对象的行为能做什么，而不是关注对象所属的类型。例如，在不使用鸭子类型的语言中，我们可以编写一个函数，它接受一个类型为"鸭子"的对象，并调用它的"走"和"叫"方法。在使用鸭子类型的语言中，这样的一个函数可以接受一个任意类型的对象，并调用它的"走"和"叫"方法。如果这些需要被调用的方法不存在，那么将引发一个运行时错误。任何拥有这样的正确的"走"和"叫"方法的对象都可被函数接受的这种行为引出了以上表述，这种决定类型的方式因此得名。

```ts
interface IPoint { 
    x:number 
    y:number 
} 
function addPoints(p1:IPoint,p2:IPoint):IPoint { 
    var x = p1.x + p2.x 
    var y = p1.y + p2.y 
    return {x:x,y:y} 
} 
 
// 正确
var newPoint = addPoints({x:3,y:4},{x:5,y:1})  
 
// 错误 
var newPoint2 = addPoints({x:1},{x:4,y:3})
```

## TypeScript 泛型

泛型（Generics）是一种编程语言特性，允许在定义函数、类、接口等时使用占位符来表示类型，而不是具体的类型。

泛型是一种在编写可重用、灵活且类型安全的代码时非常有用的功能。

使用泛型的主要目的是为了处理不特定类型的数据，使得代码可以适用于多种数据类型而不失去类型检查。

**泛型的优势包括：**

- **代码重用：** 可以编写与特定类型无关的通用代码，提高代码的复用性。
- **类型安全：** 在编译时进行类型检查，避免在运行时出现类型错误。
- **抽象性：** 允许编写更抽象和通用的代码，适应不同的数据类型和数据结构。

### 1 泛型标识符

在泛型中，通常使用一些约定俗成的标识符，比如常见的 `T`（表示 Type）、`U`、`V` 等，但实际上你可以使用任何标识符。

**T**: 代表 "Type"，是最常见的泛型类型参数名。

```ts
function identity<T>(arg: T): T {
    return arg;
}
```

**K, V**: 用于表示键（Key）和值（Value）的泛型类型参数。

```ts
interface KeyValuePair<K, V> {
    key: K;
    value: V;
}
```

**E**: 用于表示数组元素的泛型类型参数。

```ts
function printArray<E>(arr: E[]): void {
    arr.forEach(item => console.log(item));
}
```

**R**: 用于表示函数返回值的泛型类型参数。

```ts
function getResult<R>(value: R): R {
    return value;
}
```

**U, V**: 通常用于表示第二、第三个泛型类型参数。

```ts
function combine<U, V>(first: U, second: V): string {
    return `${first} ${second}`;
}
```

这些标识符是约定俗成的，实际上你可以选择任何符合标识符规范的名称。关键是使得代码易读和易于理解，所以建议在泛型类型参数上使用描述性的名称，以便于理解其用途。

### 2 泛型函数（Generic Functions）

使用泛型来创建一个可以处理不同类型的函数：

```ts
function identity<T>(arg: T): T {
    return arg;
}

// 使用泛型函数
let result = identity<string>("Hello");
console.log(result); // 输出: Hello

let numberResult = identity<number>(42);
console.log(numberResult); // 输出: 42
```

**解析：** 以上例子中，`identity` 是一个泛型函数，使用 `<T>` 表示泛型类型。它接受一个参数 `arg` 和返回值都是泛型类型 `T`。在使用时，可以通过尖括号 `<>` 明确指定泛型类型。第一个调用指定了 `string` 类型，第二个调用指定了 `number` 类型。

### 3 泛型接口（Generic Interfaces）

可以使用泛型来定义接口，使接口的成员能够使用任意类型：

```ts
// 基本语法
interface Pair<T, U> {
    first: T;
    second: U;
}

// 使用泛型接口
let pair: Pair<string, number> = { first: "hello", second: 42 };
console.log(pair); // 输出: { first: 'hello', second: 42 }
```

### 4 泛型类（Generic Classes）

泛型也可以应用于类的实例变量和方法

```ts
// 基本语法
class Box<T> {
    private value: T;

    constructor(value: T) {
        this.value = value;
    }

    getValue(): T {
        return this.value;
    }
}

// 使用泛型类
let stringBox = new Box<string>("TypeScript");
console.log(stringBox.getValue()); // 输出: TypeScript
```

**解析：** 在这个例子中，`Box` 是一个泛型类，使用 `<T>` 表示泛型类型。构造函数和方法都可以使用泛型类型 `T`。通过实例化 `Box<string>`，我们创建了一个存储字符串的 `Box` 实例，并通过 `getValue` 方法获取了存储的值。


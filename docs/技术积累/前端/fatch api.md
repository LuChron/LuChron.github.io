## Fetch API

Fetch API 是一种现代的、功能强大的网络请求工具，它允许你通过 JavaScript 异步地请求资源，而不需要使用传统的 XMLHttpRequest 对象。

Fetch API 可以简洁地发起 HTTP 请求，并处理服务器的响应。

Fetch API 基于 Promise 设计，使得异步操作更加简洁和易于理解。

> 就是前端用来获取后端数据的。

**Fetch 优点：**

- 基于 **Promises**，代码更加简洁和易读。
- 更好的错误处理机制：只在网络错误（如无法连接服务器）时返回 `catch`，而非状态码错误。
- 支持多种数据格式（JSON、文本、二进制等）。
- 可以处理跨域请求，通过 `CORS` 机制配置。

## fetch 的基本用法

fetch 的语法相当简洁，最基本的形式是：

```js
fetch(url)
  .then(response => response.json()) // 解析 JSON 数据
  .then(data => console.log(data))   // 处理数据
  .catch(error => console.error('Error:', error)); // 错误处理
```

具体意思就是：

```js
fetch(url)
  ↓ 发起网络请求
.then(response => response.json())
  ↓ 解析响应为 JSON
.then(data => 处理这个 JSON 数据)```
  ↓ 如果上面任何一步出错
.catch(error => 错误处理)
```

## 使用 Fetch

**1、基本 GET 请求：**

```js
fetch('https://api.example.com/data')
    .then(response => response.json())
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

在这个例子中，fetch 默认执行 GET 请求，返回的 response 是一个 Response 对象，通过调用 .json() 方法来解析 JSON 数据。

**2、发送 POST 请求：**

```js
fetch('https://api.example.com/data', {
    method: 'POST', // 指定请求方法
    headers: {
        'Content-Type': 'application/json'
    },
    body: JSON.stringify({
        key: 'value'
    })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

这里，我们通过设置 method 为 'POST' 来发送 POST 请求，并在请求体 body 中发送 JSON 格式的数据。

**3、处理响应状态：**

```js
fetch('https://api.example.com/data')
    .then(response => {
        if (!response.ok) {
            throw new Error('Network response was not ok ' + response.statusText);
        }
        return response.json();
    })
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

在处理响应时，我们首先检查响应状态是否成功（response.ok），如果不成功则抛出错误。

**4、发送带凭据的请求：**

```js
fetch('https://api.example.com/data', {
    credentials: 'include' // 包括 cookies 在请求中
});
```

使用 credentials: 'include' 可以在跨域请求中发送 cookies。

**5、使用 Request 和 Response 对象：**

```js
const request = new Request('flowers.jpg');
fetch(request)
    .then(response => response.blob())
    .then(imageBlob => {
        const imageObjectUrl = URL.createObjectURL(imageBlob);
        img.src = imageObjectUrl;
    });
```

你可以创建 Request 对象来定制请求，fetch 会返回一个 Response 对象，你可以用它来获取不同类型的响应体，如 blob、text、json 等。

**6、错误处理：**

```js
fetch('https://api.example.com/data')
    .then(response => {
        if (response.ok) {
            return response.json();
        }
        throw new Error('Something went wrong');
    })
    .then(data => console.log(data))
    .catch(error => console.error('Error:', error));
```

在链式调用中，任何地方抛出的错误都会被 .catch() 捕获。

**7、设置请求头**

可以通过 headers 属性为请求添加自定义的 HTTP 头信息，例如 Content-Type、Authorization 等。

```js
fetch('https://example.com/api', {
    method: 'POST',
    headers: {
        'Content-Type': 'application/json',
        'Authorization': 'Bearer your-token'
    },
    body: JSON.stringify({ name: 'John', age: 30 })
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

**8、处理非 200 的响应状态**

fetch 不会自动将 HTTP 错误状态（如 404 或 500）作为拒绝的 Promise，仍然需要检查响应状态。

```js
fetch('https://example.com/api')
  .then(response => {
    if (!response.ok) { // 检查响应状态
      throw new Error('Network response was not ok ' + response.statusText);
    }
    return response.json();
  })
  .then(data => console.log(data))
  .catch(error => console.error('Fetch error:', error));
```

**9、发送表单数据**

可以使用 FormData 对象将表单数据发送给服务器：

```js
const formData = new FormData();
formData.append('username', 'John');
formData.append('email', 'john@example.com');

fetch('https://example.com/api/form', {
    method: 'POST',
    body: formData
})
.then(response => response.text())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```

**10、跨域请求**

如果需要进行跨域请求，可以在服务器端设置 CORS（Cross-Origin Resource Sharing）。在前端，也可以通过 credentials 选项来指定是否发送 cookies 等凭据。

```js
fetch('https://example.com/api', {
    method: 'GET',
    credentials: 'include' // 允许跨域请求时携带 cookie
})
.then(response => response.json())
.then(data => console.log(data))
.catch(error => console.error('Error:', error));
```


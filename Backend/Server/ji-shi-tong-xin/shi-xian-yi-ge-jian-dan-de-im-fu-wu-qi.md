# 实现一个简单的IM服务器

实现一个简单的即时通讯（IM）服务器可以使用不同的技术栈。这里我将给出一个基于 **Node.js** 和 **Socket.IO** 的简单 IM 服务器的实现示例。该示例将支持基本的用户连接、发送消息和广播消息的功能。

测试的代码 ： [https://github.com/hly-code-source/chat-example](https://github.com/hly-code-source/chat-example)

#### 1. 环境准备

确保你的系统已经安装了 **Node.js**。可以在命令行中运行以下命令来检查是否已安装：

```bash
node -v
npm -v
```

如果未安装，请访问 [Node.js 官网](https://nodejs.org/) 下载并安装。

#### 2. 创建项目

在命令行中创建一个新的文件夹并初始化一个新的 Node.js 项目：

```bash
mkdir simple-im-server
cd simple-im-server
npm init -y
```

#### 3. 安装 Socket.IO

在项目目录中，安装 `Socket.IO` 库：

```bash
npm install socket.io express
```

#### 4. 创建服务器

在项目目录中创建一个 `server.js` 文件，并添加以下代码：

```javascript
const express = require('express');
const http = require('http');
const socketIo = require('socket.io');

const app = express();
const server = http.createServer(app);
const io = socketIo(server);

// 静态文件服务
app.use(express.static('public'));

// 连接处理
io.on('connection', (socket) => {
    console.log('A user connected:', socket.id);

    // 监听消息
    socket.on('chat message', (msg) => {
        console.log('Message received:', msg);
        // 广播消息到其他用户
        socket.broadcast.emit('chat message', msg);
    });

    // 用户断开连接
    socket.on('disconnect', () => {
        console.log('User disconnected:', socket.id);
    });
});

// 启动服务器
const PORT = process.env.PORT || 3000;
server.listen(PORT, () => {
    console.log(`Server is running on http://localhost:${PORT}`);
});
```

#### 5. 创建客户端

在项目目录中创建一个名为 `public` 的文件夹，并在其中创建一个 `index.html` 文件，添加以下代码：

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Simple IM Server</title>
    <script src="/socket.io/socket.io.js"></script>
    <script>
        document.addEventListener('DOMContentLoaded', () => {
            const socket = io();

            const form = document.getElementById('message-form');
            const input = document.getElementById('message-input');
            const messages = document.getElementById('messages');

            form.addEventListener('submit', (e) => {
                e.preventDefault(); // 防止页面刷新
                const msg = input.value;
                socket.emit('chat message', msg); // 发送消息
                input.value = ''; // 清空输入框
                return false;
            });

            // 监听消息
            socket.on('chat message', (msg) => {
                const item = document.createElement('li');
                item.textContent = msg;
                messages.appendChild(item);
                window.scrollTo(0, document.body.scrollHeight); // 滚动到底部
            });
        });
    </script>
</head>
<body>
    <ul id="messages"></ul>
    <form id="message-form">
        <input id="message-input" autocomplete="off" /><button>Send</button>
    </form>
</body>
</html>
```

#### 6. 运行服务器

在项目根目录下，运行以下命令启动服务器：

```bash
node server.js
```

#### 7. 访问应用

打开浏览器并访问 [http://localhost:3000](http://localhost:3000)。你应该会看到一个简单的聊天界面。

#### 8. 测试

在多个浏览器窗口或标签页中打开相同的地址，输入消息并发送，你会看到消息在所有连接的客户端中广播。

#### 总结

这个简单的 IM 服务器演示了如何使用 Node.js 和 Socket.IO 实现基本的实时聊天功能。你可以根据需求扩展更多功能，例如用户认证、消息持久化、文件传输等。


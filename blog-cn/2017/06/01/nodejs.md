# Node.js

****

- **[什么是Node.js](#definition)**
- **[Node.js 的特点](#feature)**
- **[安装 Node.js & NPM](#install)**
- **Node.js Demo**
- **File System API**
- **Networking with Sockets**
- **Robust Messaging Service**
- **Accessing Database**
- **Scalable Web Service**
- **Web Apps**
- **References**




### 什么是 Node.js?{#definition}

Node.js使用C++语言编写而成, 是一个后端的Javascript的运行环境, 同时还提供了很多系统级的API, 比如文件操作, 网络编程等, 支持的系统包括*nux, Windows.所以可以编写系统级或者服务器端的JavaScript代码, 交给Node.js来编译执行.



> 为什么采用C++语言呢?
>
> 据Node.js创始人Ryan Dahl回忆, 他最初希望采用Ruby来写Node.js, 但是后来发现Ruby虚拟机的性能不能满足他的要求, 后来尝试采用V8引擎, 所以选择了C++语言.

> [V8引擎](https://zh.wikipedia.org/wiki/V8_(JavaScript%E5%BC%95%E6%93%8E))
>
> V8是由Google开发并开源的JavaScript引擎, 用于Google Chrome中.
>
> V8在运行之前将JavaScript编译成机器码而非字节码或是解释执行它, 以提升性能. 更进一步, 使用了如内联缓存 (inline caching) 等方法来提高性能. 有了这些性能, JavaScript程序与V8引擎的速度媲美二进制编译.

> [JavaScript引擎](https://zh.wikipedia.org/wiki/JavaScript%E5%BC%95%E6%93%8E)
>
> JavaScript引擎是一个专门处理JavaScript脚本的虚拟机, 一般会附带在浏览器中.
>
> JavaScript引擎能为程序员提供部分操作浏览器的功能 (网络, DOM, 外部事件, HTML5视频, Canvas和存储).
>
> 其他JavaScript引擎:
>
> SpiderMonkey, 第一款问世的JavaScript引擎, 现由Mozilla基金会维护, 用于FireFox.
>
> JavaScriptCore, 开放源代码, 用于Safari.
>
> Chakra, 用于Microsoft Edge.



###Node.js 的特点{#feature}

- 异步编程
- 事件驱动
- 单进程, 单线程模式运行
- 轻量, 高效

> [高效](http://taobaofed.org/blog/2015/10/29/deep-into-node-1/):
>
> Node.js的作者除了使用V8作为JavaScript引擎之外, 还是用了高效的libev和libeio库支持事件驱动和异步式I/O
>
> Node.js的开发者在libev和libeio的基础上还抽象除了libuv层, 对于POSIX操作系统, libuv 通过封装libev和libeio来利用epoll和kqueue. 而在Windows下, libuv使用了Windows的IOCP (Input/Output Completion Port, 输入输出完成接口)机制, 以在不同的平台下实现同样的高性能.



> POSIX (Portable Operating System Interface) 是一套操作系统API规范, 一般而言, 遵守POSIX规范的操作系统指的是UNIX, Linux, Mac OS X等.



### 安装Node.js和NPM{#install}

Windows下安装Node.js步骤:

- [下载Node.js安装包](https://nodejs.org/en/download/)

- 运行安装文件.

- 根据安装向导安装Node.js

- 安装完成后, 打开命令行工具运行命令来检查是否安装成功.

  ```
  node -v
  ```

  ```
  npm -v
  ```

### Demo{#demo}


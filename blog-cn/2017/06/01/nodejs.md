

# Node.js

****

- **[什么是Node.js](#什么是-nodejs)**
- **[Node.js架构](#nodejs-架构)**
- **[Node.js 工作流程图](#nodejs-工作流程图)**
- **[Node.js 的特点](#nodejs-的特点)**
- **[Node.js 的缺点](#nodejs-的缺点)**
- **[Node.js 的应用场景](#nodejs-的应用场景)**
- **[安装 Node.js & NPM](#安装-nodejs--npm)**
- **[Node.js Demo](#demo)**
- **[SuperVisor](#supervisor)**
- **[模块和包](#模块和包)**
- **[Node.js 包管理器(NPM)](#nodejs-包管理器(NPM))**




### 什么是 Node.js?

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
>



### Node.js 架构

![Node.js内部架构图](https://i.stack.imgur.com/u1O2O.png)



[**其他 C/C++ 组件和库**](https://nodejs.org/en/docs/meta/topics/dependencies/)：如 [c-ares](http://c-ares.haxx.se/)、[crypto (OpenSSL)](https://www.openssl.org/)、[http-parser](https://github.com/nodejs/http-parser) 以及 [zlib](http://zlib.net/)。这些依赖提供了对系统底层功能的访问，包括网络、压缩、加密等。

**应用/模块（Application/Modules）**：这部分就是所有的 JavaScript 代码：你的应用程序、Node.js 核心模块、任何 npm install 的模块，以及你写的所有模块代码。你花费的主要精力都在这部分。

**绑定（Bindings）**：Node.js 用了这么多 C/C++ 的代码和库，简单来说，它们性能很好。不过，JavaScript 代码最后是怎么跟这些 C/C++ 代码互相调用的呢？这不是三种不同的语言吗？确实如此，而且通常不同语言写出来的代码也不能互相沟通，没有 binding 就不行。Binding 是一些胶水代码，能够把不同语言绑定在一起使其能够互相沟通。在 Node.js 中，binding 所做的就是把 Node.js 那些用 C/C++ 写的库接口暴露给 JS 环境。这么做的目的之一是代码重用：这些功能已经有现存的成熟实现，没必要只是因为换个语言环境就重写一遍，如果桥接调用一下就足够的话。另一个原因是性能：C/C++ 这样的系统编程语言通常都比其他高阶语言（Python、JavaScript、Ruby 等等）性能更高，所以把主要消耗 CPU 的操作以 C/C++ 代码来执行更加明智。

**C/C++ Addons**：Binding 仅桥接 Node.js 核心库的一些依赖，zlib、OpenSSL、c-ares、http-parser 等。如果你想在应用程序中包含其他第三方或者你自己的 C/C++ 库的话，需要自己完成这部分胶水代码。你写的这部分胶水代码就称为 Addon。可以把 Binding 和 Addon 视为连接 JavaScript 代码和 C/C++ 代码的桥梁

###  Node.js 工作流程图

![Node.js 工作流程图](https://i.stack.imgur.com/QRePV.jpg)

一个 Node.js 应用启动时，V8 引擎会执行你写的应用代码，保持一份观察者（注册在事件上的处理函数）列表。当事件发生时，它的处理函数会被加进一个**事件队列**。只要这个队列还有等待执行的事件，**事件循环**就会持续把事件从队列中拿出，放进**调用堆栈**。需要注意的是，只有当前一个事件处理完毕（调用堆栈也已经清空），事件循环才会把下一个事件放进调用堆栈。

在调用堆栈中，所有的 I/O 请求都会转发给 libuv 处理。libuv 会维持一个线程池，包含四个工作线程（这是默认数量，也可以修改配置增加更多工作线程）。文件系统 I/O 请求和 DNS 相关请求都会放进这个线程池处理；其他的请求，如网络、平台特性相关的请求会分发给相应的系统处理单元（参见 [libuv 设计概览](http://docs.libuv.org/en/v1.x/design.html)）。

安排给线程池的这些 I/O 操作由 Node.js 的底层库执行，完成之后 libuv 把此事件放回事件队列，等待主线程执行后续操作。在 libuv 处理这些异步 I/O 操作期间，主线程不会等待处理结果，而是继续忙其他事情，只有当事件循环把 libuv 返回的事件放进调用堆栈之后，主线程才会继续处理这个事件的后续操作。这就是一个事件在 Node.js 中执行的整个生命周期。



### Node.js 的特点

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



### Node.js 的缺点

- 不适合CPU密集型应用
- 只支持单核CPU, 不能充分利用多核CPU
- 可靠性低, 一旦代码某个环节崩溃, 整个系统都会崩溃
- 开源组件库质量参差不齐, 更新快, 不向下兼容



> NOTE:
>
> Just because Node is designed without threads, doesn't mean you cannot take advantage of multiple cores in your environment. Child processes can be spawned by using our [`child_process.fork()`](https://nodejs.org/api/child_process.html#child_process_child_process_fork_modulepath_args_options) API, and are designed to be easy to communicate with. Built upon that same interface is the [`cluster`](https://nodejs.org/api/cluster.html) module, which allows you to share sockets between processes to enable load balancing over your cores.



### Node.js 的应用场景

- RESTful API
- 单页面, 多Ajax请求应用
- 命令行工具
- 流式数据 (比如实时文件上传系统)
- 准实时应用系统 (比如聊天系统, 微博系统)

### 安装 Node.js & NPM

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

### Demo

- Hello World
- HTTP 服务器
- 读取文件
- EventEmitter

> Node.js 命令行工具
>
> ```
> node script.js
> ```
>
> ```
> node --help
> ```
>
> Node的REPL模式
>
> REPL (Read-eval-print loop), 即输入-运算执行-输出-循环



### SuperVisor

在开发Node.js HTTP Server 时, 无论你修改了代码的哪一部分, 都必须终止Node.js, 在重新运行才会奏效.

这是因为Node.js 只有在第一次引用到某部分时才会去解析脚本文件, 以后都会直接访问内存, 避免重新载入.

Node.js的这种设计虽然有利于提高性能, 但是不利于开发调试. 因为我们在开发过程中总是希望修改后, 立即看到效果, 而不是每次都终止进程并重启. 

SuperVisor可以帮你实现这个功能, 它会监视代码的改动, 并自动重启Node.js.

可以通过下面的命令安装SuperVisor

```
npm install supervisor -g
```

然后使用supervisor命令启动app.js

```
supervisor app.js
```



### 模块和包

模块(Module)和包(package)是Node.js最重要的支柱. 开发一个具有一定规模的程序不可能只用一个文件, 通常需要把各个功能拆分, 封装, 然后组合起来, 模块正是为了实现这种方式而诞生的.

Node.js 提供了 require 函数来调用其他模块, 而且模块都是基于文件的, 机制十分简单.

- 什么是模块

模块是 Node.js 应用程序的基本组成部分，文件和模块是一一对应的。换言之，一个Node.js 文件就是一个模块,这个文件可能是 JavaScript 代码、JSON 或者编译过的 C/C++ 扩展。
在前面的例子中，我们曾经用到了 var http = require('http')，其中 http
是 Node.js 的一个核心模块，其内部是用 C++ 实现的，外部用 JavaScript 封装。我们通过
require 函数获取了这个模块，然后才能使用其中的对象。

- 创建及加载模块

  - 创建模块

    在 Node.js 中，创建一个模块非常简单，因为一个文件就是一个模块，我们要关注的问
    题仅仅在于如何在其他文件中获取这个模块。Node.js 提供了 exports 和 require 两个对
    象，其中 exports 是模块公开的接口，require 用于从外部获取一个模块的接口，即所获
    取模块的 exports 对象。

    demo

    **mymodule**.js

    ```

    var name;

    exports.setName=(theName)=>{
        name=theName;
    }

    exports.sayHello=()=>{
        console.log(`Hello ${name}`)
    }
    ```

    **mymoduledemo**.js

    ```
    var myModule=require('./mymodule');
    myModule.setName('Ken');
    myModule.sayHello();
    ```

    > NOTE
    > 在这个示例中, mymodule.js 通过exports对象把setName和sayHello作为模块的访问接口.
    >
    > 在mymoduledemo.js 中, 通过require('./mymodule') 来加载模块, 然后就可以访问mymodule.js 中exports 对象的成员函数了.

  - 单次加载

    上面的例子中有点类似创建一个对象, 但实际上和对象又有本质的区别. 因为**require不会重复加载模块**, 也就是说无论调用多少次require, 获得的模块都是**同一个**.

    demo, 然后检查运算结果.

    ```
    var myModule=require('./mymodule');
    myModule.setName('Ken');

    var myModule2=require('./mymodule');
    myModule.setName('Ben');

    myModule.sayHello();
    myModule2.sayHello();
    ```


-   覆盖exports

    通过exports.xxx=xxx 来覆盖exports, 然后new 来实例化不同的对象.

    > NOTE:
    >
    > 事实上，exports 本身仅仅是一个普通的空对象，即 {}，它专门用来声明接口，本
    > 质上是通过它为模块闭包①的内部建立了一个有限的访问接口。因为它没有任何特殊的地方，
    > 所以可以用其他东西来代替

    > Warning:
    >
    > 不可以通过对 exports 直接赋值代替对 module.exports 赋值。
    > exports 实际上只是一个和 module.exports 指向同一个对象的变量，
    > 它本身会在模块执行结束后释放，但 module 不会，因此只能通过指定
    > module.exports 来改变访问接口


- 创建包

  包是在模块基础上更深一步的抽象，Node.js 的包类似于 C/C++ 的函数库或者 Java/.Net
  的类库。它将某个独立的功能封装起来，用于发布、更新、依赖管理和版本控制。Node.js 根
  据 CommonJS 规范实现了包机制，开发了 npm来解决包的发布和获取需求。
  Node.js 的包是一个目录，其中包含一个 JSON 格式的包说明文件 package.json。严格符
  合 CommonJS 规范的包应该具备以下特征：

  - package.json必须在包的顶层目录下;
  - 二进制文件应该在 bin 目录下;
  -  JavaScript 代码应该在 lib 目录下;
  - 文档应该在 doc 目录下;
  - 单元测试应该在 test 目录下;

  Node.js 对包的要求并没有这么严格，只要顶层目录下有 package.json，并符合一些规范
  即可。**当然为了提高兼容性，我们还是建议你在制作包的时候，严格遵守 CommonJS 规范**。

  我们使用这种方法可以把文件夹封装为一个模块，即所谓的包。包通常是一些模块的集
  合，在模块的基础上提供了更高层的抽象，相当于提供了一些固定接口的函数库。通过定制
  package.json，我们可以创建更复杂、更完善、更符合规范的包用于发布.

  > NOTE:
  >
  > 通过执行下面的命令可以轻松创建package.json
  >
  > ```
  > npm init
  > ```




### Node.js 包管理器(NPM)


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
- **[Node.js 包管理器(NPM)](#nodejs-包管理器npm)**
- **[模块加载机制](#模块加载机制)**




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
  - JavaScript 代码应该在 lib 目录下;
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

Node.js包管理器，即npm是 Node.js 官方提供的包管理工具，它已经成了 Node.js 包的
标准发布平台，用于 Node.js 包的发布、传播、依赖控制。npm 提供了命令行工具，使你可
以方便地下载、安装、升级、删除包，也可以让你作为开发者发布并维护包。



**本地模式和全局模式**

npm在默认情况下会从http://npmjs.org搜索或下载包，将包安装到当前目录的node_modules
子目录下。

在使用 npm 安装包的时候，有两种模式：本地模式和全局模式。默认情况下我们使用 npm
install命令就是采用本地模式，即把包安装到当前目录的 node_modules 子目录下。Node.js
的 require 在加载模块时会尝试搜寻 node_modules 子目录，因此使用 npm 本地模式安装
的包可以直接被引用。
npm 还有另一种不同的安装模式被成为全局模式，使用方法为：
npm [install/i] -g [package_name]
与本地模式的不同之处就在于多了一个参数 -g。我们在 介绍 supervisor那个小节中使用
了 npm install -g supervisor 命令，就是以全局模式安装 supervisor。
为什么要使用全局模式呢？多数时候并不是因为许多程序都有可能用到它，为了减少多
重副本而使用全局模式，而是因为本地模式不会注册 PATH 环境变量。举例说明，我们安装
supervisor 是为了在命令行中运行它，譬如直接运行 supervisor script.js，这时就需要在 PATH
环境变量中注册 supervisor。npm 本地模式仅仅是把包安装到 node_modules 子目录下，其中
的 bin 目录没有包含在 PATH 环境变量中，不能直接在命令行中调用。而当我们使用全局模
式安装时，npm 会将包安装到系统目录，譬如 /usr/local/lib/node_modules/，同时 package.json 文
件中 bin 字段包含的文件会被链接到 /usr/local/bin/。/usr/local/bin/ 是在PATH 环境变量中默认
定义的，因此就可以直接在命令行中运行 supervisor script.js命令了。

总而言之，当我们要把某个包作为工程运行时的一部分时，通过本地模式获取，如果要
在命令行下使用，则使用全局模式安装。



**发布包**

在发布前，我们还需要获得一个账号用于今后维护自己的包，使用 npm adduser 根据
提示输入用户名、密码、邮箱，等待账号创建完成。完成后可以使用 npm whoami 测验是
否已经取得了账号。

接下来，在 package.json 所在目录下运行 npm publish，稍等片刻就可以完成发布了。
打开浏览器，访问 https://www.npmjs.com/~{username} 就可以找到自己刚刚发布的包了。现在我们可以在
世界的任意一台计算机上使用 npm install byvoidmodule 命令来安装它。

如果你的包将来有更新，只需要在 package.json 文件中修改 version 字段，然后重新
使用 npm publish 命令就行了。如果你对已发布的包不满意（比如我们发布的这个毫无意
义的包），可以使用 npm unpublish 命令来取消发布。



### 模块加载机制

Node.js的模块加载对用户来说十分简单, 只需要调用require即可, 但是内部机制呢?

模块的类型:

- 原生(核心)模块
- 文件模块

原生模块在Node.js源代码编译的时候编译进了二进制执行文件, 加载的速度最快.

文件模块是动态加载的, 加载速度比原生模块慢.

但是Node.js对原生模块和文件模块都进行了缓存, 于是在第二次require时, 是不会有重复开销的. 

**一般情况下是不会重复, 但是一些情况下还是会重复. 具体可以看** [Node.js中相同模块是否会被加载多次？](http://blog.zhaojie.me/2011/12/same-node-module-load-multiple-times.html)

> 模块缓存的注意事项
>
> 模块是基于其解析的文件名进行缓存的。由于调用模块的位置的不同，模块可能被解析成不同的文件名（比如从 `node_modules` 目录加载），这样就不能保证 `require('foo')` 总能返回完全相同的对象。
>
> 此外，在不区分大小写的文件系统或操作系统中，被解析成不同的文件名可以指向同一文件，但缓存仍然会将它们视为不同的模块，并多次重新加载。例如，`require('./foo')` 和 `require('./FOO')` 返回两个不同的对象，而不会管 `./foo` 和 `./FOO` 是否是相同的文件。



强烈建议将所有的依赖放在本地的 `node_modules` 目录。这样将会更快地加载，且更可靠

> 原生模块
>
> 原生模块就是Node.js标准API中提供的模块, 如 fs, http, net , vm 等, 这些都是由Node.js官方提供的模块, 编译成了二进制代码.
>
> 我们可以直接通过require获取原生模块, 例如 require('fs')
>
> 原生模块拥有最高的加载优先级, 换言之如果有模块与其命名冲突, Node.js总是会加载原生模块.



> 文件模块
>
> 文件模块这是存储为单独的文件或文件夹的模块, 可能是Javascript代码, JSON 或编译好的C/C++代码.
>
> 文件模块的加载方法相对复杂(按路径加载和查找node_modules文件夹), 但十分灵活, 尤其和npm结合使用时.
>
> 在不显示指定文件模块扩展名的时候, Node.js会分别试图加上.js, .json 或 .node扩展名



>.js 是 Javascript代码, 通过fs模块同步读取js文件并编译执行.
>
>.json 是JSON格式的文本, 读取文件, 调用JSON.parse解析加载.
>
>.node是编译好的C/C++代码, 通过C/C++进行编写的Addon. 通过dlopen方法进行加载.



**按路径加载模块**

如果require参数以 ''/' 开头, 表明以绝对路径的方式查找模块.

如果require参数以 ''./" 或 "../" 开头, 那么则以相对路径的方式查找模块.



**查找 node_modules 目录加载模块**

如果require参数不以 "/", "./", "../" 开头, 而该模块又不是核心模块, 那么就需要查找 node_modules 加载模块.

我们使用npm获取的包通常就是使用这种方式加载的.

当 require 遇到一个既不是核心模块，又不是以路径形式表示的模块名称时，会试图
在当前目录下的 node_modules 目录中来查找是不是有这样一个模块。如果没有找到，则会
在当前目录的上一层中的 node_modules 目录中继续查找，反复执行这一过程，直到遇到根
目录为止.



**加载缓存**

我们在前面提到过，Node.js 模块不会被重复加载，这是因为 Node.js 通过文件名缓存所
有加载过的文件模块，所以以后再访问到时就不会重新加载了。注意，Node.js 是根据实际文
件名缓存的， 而不是 require() 提供的参数缓存的， 也就是说即使你分别通过
require('express') 和 require('./node_modules/express') 加载两次，也不会重
复加载，因为尽管两次参数不同，解析到的文件却是同一个。



**加载顺序**

下面总结一下使用 require(some_module) 时的加载顺序。
(1) 如果some_module 是一个核心模块，直接加载，结束。
(2) 如果some_module以“ / ”、“ ./ ”或“ ../ ”开头，按路径加载 some_module，结束。
(3) 假设当前目录为 current_dir，按路径加载 current_dir/node_modules/some_module。
 如果加载成功，结束。
 如果加载失败，令current_dir为其父目录。
 重复这一过程，直到遇到根目录，抛出异常，结束



> Note:
>
> [浅析NodeJS模块加载机制](https://github.com/muwenzi/Program-Blog/issues/94)
>
> [深入Node.js的模块机制](http://www.infoq.com/cn/articles/nodejs-module-mechanism)

![Node modules 加载步骤](http://www.infoq.com/resource/articles/nodejs-module-mechanism/zh/resources/image1.jpg)

**模块包装器**

在执行模块代码之前，Node.js 会使用一个如下的函数包装器将其包装：

```
(function(exports, require, module, __filename, __dirname) {
// 模块的代码实际上在这里
});
```

通过这样做，Node.js 实现了以下几点：

- 它保持了顶层的变量（用 `var`、`const` 或 `let` 定义）作用在模块范围内，而不是全局对象。
- 它有助于提供一些看似全局的但实际上是模块特定的变量，例如：
  - 实现者可以使用 `module` 和 `exports` 对象从模块中导出值。
  - 快捷变量 `__filename` 和 `__dirname` 包含模块的绝对文件名和目录路径。


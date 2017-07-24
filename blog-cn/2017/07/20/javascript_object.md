# ECMAScript对象

- **[面向对象](#面向对象)**
- **[对象应用](#对象的应用)**
- **[对象类型](#对象类型)**
- **[对象作用域](#对象作用域)**
- **[定义类和对象](#定义类或对象)**
- **修改对象**



### 面向对象

**面向对象语言的要求**
一种面向对象语言需要向开发者提供四种基本能力：

1. 封装 - 把相关的信息（无论数据或方法）存储在对象中的能力
2. 聚集 - 把一个对象存储在另一个对象内的能力
3. 继承 - 由另一个类（或多个类）得来类的属性和方法的能力
4. 多态 - 编写能以多种方法运行的函数或方法的能力

ECMAScript 支持这些要求，因此可被是看做面向对象的。



**对象的构成**

在 ECMAScript 中，对象由特性（attribute）构成，特性可以是原始值，也可以是引用值。如果特性存放的是函数，它将被看作对象的方法（method），否则该特性被看作对象的属性（property）。



> ECMA
>
> ECMA是“European Computer Manufactures Association”的缩写，中文称欧洲计算机制造联合会。是1961年成立的旨在建立统一的电脑操作格式标准--包括程序语言和输入输出的组织。
>
> 这个组织的目标是评估，开发和认可电信和计算机标准。主要任务是研究信息和通讯技术方面的标准并发布有关技术报告。ECMA并不是官方机构，而是由主流厂商组成的，他们经常与其他国际组织进行合作。

> ECMAScript
>
> ECMAscript是基于Netscape JavaScript的一种标准[脚本语言](https://baike.baidu.com/item/%E8%84%9A%E6%9C%AC%E8%AF%AD%E8%A8%80)。它也是一种基于对象的语言，通过DOM可以操作网页上的任何对象。可以增加、删除、移动或者改变对象。使得网页的[交互性](https://baike.baidu.com/item/%E4%BA%A4%E4%BA%92%E6%80%A7/10758528)大大提高。



### **对象的应用**

**对象的创建和销毁都在 JavaScript 执行过程中发生，理解这种范式的含义对理解整个语言至关重要。**

**声明和实例化**

对象的创建方式是用关键字 new 后面跟上实例化的类的名字：

```
var oObject = new Object();
var oStringObject = new String();
```

第一行代码创建了 Object 类的一个实例，并把它存储到变量 oObject 中。第二行代码创建了 String 类的一个实例，把它存储在变量 oStringObject 中。**如果构造函数无参数，括号则不是必需的**。因此可以采用下面的形式重写上面的两行代码：

```
var oObject = new Object;
var oStringObject = new String;

```

**对象引用**

在 ECMAScript 中，不能访问对象的物理表示，只能访问对象的引用。每次创建对象，存储在变量中的都是该对象的引用，而不是对象本身。

**对象废除**

ECMAScript 拥有无用存储单元收集程序（garbage collection routine），意味着不必专门销毁对象来释放内存。当再没有对对象的引用时，称该对象被废除（dereference）了。运行无用存储单元收集程序时，所有废除的对象都被销毁。每当函数执行完它的代码，无用存储单元收集程序都会运行，释放所有的局部变量，还有在一些其他不可预知的情况下，无用存储单元收集程序也会运行。

把对象的所有引用都设置为 null，可以强制性地废除对象。例如：

```
var oObject = new Object;
// do something with the object here
oObject = null;

```

当变量 oObject 设置为 null 后，对第一个创建的对象的引用就不存在了。这意味着下次运行无用存储单元收集程序时，该对象将被销毁。

每用完一个对象后，就将其废除，来释放内存，这是个好习惯。这样还确保不再使用已经不能访问的对象，从而防止程序设计错误的出现。此外，旧的浏览器（如 IE/MAC）没有全面的无用存储单元收集程序，所以在卸载页面时，对象可能不能被正确销毁。废除对象和它的所有特性是确保内存使用正确的最好方法。

注意：废除对象的所有引用时要当心。如果一个对象有两个或更多引用，则要正确废除该对象，必须将其所有引用都设置为 null。

**早绑定和晚绑定**

所谓绑定（binding），即把对象的接口与对象实例结合在一起的方法。

早绑定（early binding）是指在实例化对象之前定义它的属性和方法，这样编译器或解释程序就能够提前转换机器代码。在 Java 和 Visual Basic 这样的语言中，有了早绑定，就可以在开发环境中使用 IntelliSense（即给开发者提供对象中属性和方法列表的功能）。ECMAScript 不是强类型语言，所以不支持早绑定。

另一方面，晚绑定（late binding）指的是编译器或解释程序在运行前，不知道对象的类型。使用晚绑定，无需检查对象的类型，只需检查对象是否支持属性和方法即可。ECMAScript 中的所有变量都采用晚绑定方法。这样就允许执行大量的对象操作，而无任何惩罚。



### 对象类型



在 ECMAScript 中, 所有对象并非同等创建的.

一般来说, 可以创建并使用的对象有三种, **本地对象**, **内置对象**和**宿主对象**.

------

**本地对象**

ECMA-262 把本地对象（native object）定义为“独立于宿主环境的 ECMAScript 实现提供的对象”。简单来说，本地对象就是 ECMA-262 定义的类（引用类型）。它们包括：

- Object
- Function
- Array
- String
- Boolean
- Number
- Date
- RegExp
- Error
- EvalError
- RangeError
- ReferenceError
- SyntaxError
- TypeError
- URIError

------

**内置对象**

ECMA-262 把内置对象（built-in object）定义为“由 ECMAScript 实现提供的、独立于宿主环境的所有对象，在 ECMAScript 程序开始执行时出现”。这意味着开发者不必明确实例化内置对象，它已被实例化了。ECMA-262 只定义了两个内置对象，即 Global 和 Math （它们也是本地对象，根据定义，每个内置对象都是本地对象）。

Global, 理解为全局对象. 

全局对象描述:

全局对象是预定义的对象, 作为JavaScript的全局函数和全局属性的占位符. 通过使用全局对象, 可以访问所有其他预定义的对象, 函数和属性. 全局对象不是任何对象的属性, 所以没有名称.

在顶层JavaScript代码中, 可以用关键字this 引用全局对象. 

但是通常不必用这种方式引用全局对象, 因为全局对象的作用域链的头, 这意味着所有非限定性的变量和函数名都会作为该对象的属性来访问. 例如: 当JavaScript代码引用parseInt()函数时, 它引用的是全局对象的parseInt函数.

全局对象是作用域链的头, 还意味着在顶层JavaScript代码中声明的所有变量都将成为全局对象的属性.

全局对象只是一个对象, 而不是类, 既没有构造方法, 也无法实例化一个新的全局对象.

在JavaScript代码嵌入一个特殊环境中时, 全局对象通常具有环境特定的属性. 实际上ECMAScript标准没有规定全局对象的类型, JavaScript的实现或嵌入的JavaScript都可以把任意类型的对象作为全局对象, 只要该对象定义了这里列出的基本属性和函数.例如: 在允许通过LiveConnect或相关的技术来脚本化Java的JavaScript实现中, 全局对象被赋予了这里列出的java和Package属性及getClass()方法. 而在客户端JavaScript中, 全局对象就是Window对象, 标识允许JavaScript代码的Web浏览器窗口.

- 顶层函数 (全局函数)
- 顶层属性 (全局属性)
- Math 对象

> Note:
>
> 全局属性和函数可用于所有内建的JavaScript对象.
>
> **顶层函数 (全局函数)**
>
> | 函数                                       | 描述                              |
> | ---------------------------------------- | ------------------------------- |
> | [decodeURI()](http://www.w3school.com.cn/jsref/jsref_decodeURI.asp) | 解码某个编码的 URI。                    |
> | [decodeURIComponent()](http://www.w3school.com.cn/jsref/jsref_decodeURIComponent.asp) | 解码一个编码的 URI 组件。                 |
> | [encodeURI()](http://www.w3school.com.cn/jsref/jsref_encodeuri.asp) | 把字符串编码为 URI。                    |
> | [encodeURIComponent()](http://www.w3school.com.cn/jsref/jsref_encodeURIComponent.asp) | 把字符串编码为 URI 组件。                 |
> | [escape()](http://www.w3school.com.cn/jsref/jsref_escape.asp) | 对字符串进行编码。                       |
> | [eval()](http://www.w3school.com.cn/jsref/jsref_eval.asp) | 计算 JavaScript 字符串，并把它作为脚本代码来执行。 |
> | [getClass()](http://www.w3school.com.cn/jsref/jsref_getClass.asp) | 返回一个 JavaObject 的 JavaClass。    |
> | [isFinite()](http://www.w3school.com.cn/jsref/jsref_isFinite.asp) | 检查某个值是否为有穷大的数。                  |
> | [isNaN()](http://www.w3school.com.cn/jsref/jsref_isNaN.asp) | 检查某个值是否是数字。                     |
> | [Number()](http://www.w3school.com.cn/jsref/jsref_number.asp) | 把对象的值转换为数字。                     |
> | [parseFloat()](http://www.w3school.com.cn/jsref/jsref_parseFloat.asp) | 解析一个字符串并返回一个浮点数。                |
> | [parseInt()](http://www.w3school.com.cn/jsref/jsref_parseInt.asp) | 解析一个字符串并返回一个整数。                 |
> | [String()](http://www.w3school.com.cn/jsref/jsref_string.asp) | 把对象的值转换为字符串。                    |
> | [unescape()](http://www.w3school.com.cn/jsref/jsref_unescape.asp) | 对由 escape() 编码的字符串进行解码。         |
>
> **顶层属性 (全局属性)**
>
> | 方法                                       | 描述                            |
> | ---------------------------------------- | ----------------------------- |
> | [Infinity](http://www.w3school.com.cn/jsref/jsref_infinity.asp) | 代表正的无穷大的数值。                   |
> | [java](http://www.w3school.com.cn/jsref/jsref_java.asp) | 代表 java.* 包层级的一个 JavaPackage。 |
> | [NaN](http://www.w3school.com.cn/jsref/jsref_nan.asp) | 指示某个值是不是数字值。                  |
> | [Packages](http://www.w3school.com.cn/jsref/jsref_Packages.asp) | 根 JavaPackage 对象。             |
> | [undefined](http://www.w3school.com.cn/jsref/jsref_undefined.asp) | 指示未定义的值。                      |



在JavaScript核心语言中, 全局对象的预定义属性都是可枚举的, 随意可以使用for/in循环出所有隐式或显式声明的全局变量.

```javascript
var variables = "";

for (var name in this) 
{
variables += name + "<br />";
}

document.write(variables);
```

[demo](showglobal.html)

------

**宿主对象**

所有非本地对象都是宿主对象(host object), 即由ECMAScript实现的宿主环境提供的对象.

所有BOM和DOM对象都是宿主对象.

> **BOM**
>
> Browser Object Model, 浏览器对象模型.
>
> BOM提供了独立于内容与浏览器窗口交互的对象.
>
> BOM主要用于管理窗口与窗口之间的通讯, 因此核心对象是window.
>
> BOM由一系列相关的对象组成, 并且每个对象都提供了很多属性和方法. 比如: windows, location, history, navigator, screen, frames, document.
>
> 通过BOM对象来访问, 控制, 修改浏览器, BOM描述了与浏览器进行交互的方法和接口.
>
> BOM缺乏标准, 因此不同的浏览器都有自己的实现.

> **DOM**
>
> Document Object Model, 文档对象模型
>
> DOM是W3C的标准, 定义了访问HTML和XML文档的标准.
>
> ​        “W3C 文档对象模型 （DOM） 是中立于平台和语言的接口，它允许程序和脚本动态地访问和更新文档的内容、结构和样式。”
>
> DOM标准被分为3个不同的部分:
>
> - 核心DOM---针对任何结构化文档的标准模型
> - XML DOM---针对XML文档的标准模型
> - HTML DOM---针对HTML文档的标准模型
>
> DOM描述了处理网页内容的方法和接口.
>
> [WiKi](https://zh.wikipedia.org/wiki/%E6%96%87%E6%A1%A3%E5%AF%B9%E8%B1%A1%E6%A8%A1%E5%9E%8B)
>
> [W3C](https://www.w3.org/TR/dom/)
>
> [JavaScript实现](http://www.w3school.com.cn/js/pro_js_implement.asp)

![BOM结构图](imgs/browser_objects_model.png)

------

### 对象作用域

作用域指的是变量的使用范围

## 公用、私有和受保护作用域

### 概念

在传统的面向对象程序设计中，主要关注于公用和私有作用域。公用作用域中的对象属性可以从对象外部访问，即开发者创建对象的实例后，就可使用它的公用属性。而私有作用域中的属性只能在对象内部访问，即对于外部世界来说，这些属性并不存在。这意味着如果类定义了私有属性和方法，则它的子类也不能访问这些属性和方法。

受保护作用域也是用于定义私有的属性和方法，只是这些属性和方法还能被其子类访问。

### ECMAScript 只有公用作用域

对 ECMAScript 讨论上面这些作用域几乎毫无意义，因为 ECMAScript 中只存在一种作用域 - 公用作用域。ECMAScript 中的所有对象的所有属性和方法都是公用的。因此，定义自己的类和对象时，必须格外小心。记住，所有属性和方法默认都是公用的！

### 建议性的解决方法

许多开发者都在网上提出了有效的属性作用域模式，解决了 ECMAScript 的这种问题。

由于缺少私有作用域，开发者确定了一个规约，说明哪些属性和方法应该被看做私有的。这种规约规定在属性前后加下划线：

```
obj._color_ = "blue";
```

这段代码中，属性 color 是私有的。注意，下划线并不改变属性是公用属性的事实，它只是告诉其他开发者，应该把该属性看作私有的。

有些开发者还喜欢用单下划线说明私有成员，例如：obj._color。

## 静态作用域

静态作用域定义的属性和方法任何时候都能从同一位置访问。在 Java 中，类可具有属性和方法，无需实例化该类的对象，即可访问这些属性和方法，例如 java.net.URLEncoder 类，它的函数 encode() 就是静态方法。

### ECMAScript 没有静态作用域

严格来说，ECMAScript 并没有静态作用域。不过，它可以给构造函数提供属性和方法。还记得吗，构造函数只是函数。函数是对象，对象可以有属性和方法。例如：

```
function sayHello() {
  alert("hello");
}

sayHello.alternate = function() {
  alert("hi");
}

sayHello();		//输出 "hello"
sayHello.alternate();	//输出 "hi"
```

> this
>
> this关键字后面单独讲解



------

### 定义类或对象

**使用预定义对象只是面向对象语言的能力的一部分，它真正强大之处在于能够创建自己专用的类和对象。**

**ECMAScript 拥有很多创建对象或类的方法。**


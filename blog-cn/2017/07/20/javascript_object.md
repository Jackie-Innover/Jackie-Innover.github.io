# ECMAScript对象

[TOC]


### 面向对象

#### 面向对象语言的要求

一种面向对象语言需要向开发者提供四种基本能力：

1. 封装 - 把相关的信息（无论数据或方法）存储在对象中的能力
2. 聚集 - 把一个对象存储在另一个对象内的能力
3. 继承 - 由另一个类（或多个类）得来类的属性和方法的能力
4. 多态 - 编写能以多种方法运行的函数或方法的能力

ECMAScript 支持这些要求，因此可被是看做面向对象的。



#### 对象的构成

在 ECMAScript 中，对象由特性（attribute）构成，特性可以是原始值，也可以是引用值。如果特性存放的是函数，它将被看作对象的方法（method），否则该特性被看作对象的属性（property）。



> ECMA
>
> ECMA是“European Computer Manufactures Association”的缩写，中文称欧洲计算机制造联合会。是1961年成立的旨在建立统一的电脑操作格式标准--包括程序语言和输入输出的组织。
>
> 这个组织的目标是评估，开发和认可电信和计算机标准。主要任务是研究信息和通讯技术方面的标准并发布有关技术报告。ECMA并不是官方机构，而是由主流厂商组成的，他们经常与其他国际组织进行合作。

> ECMAScript
>
> ECMAscript是基于Netscape JavaScript的一种标准[脚本语言](https://baike.baidu.com/item/%E8%84%9A%E6%9C%AC%E8%AF%AD%E8%A8%80)。它也是一种基于对象的语言，通过DOM可以操作网页上的任何对象。可以增加、删除、移动或者改变对象。使得网页的[交互性](https://baike.baidu.com/item/%E4%BA%A4%E4%BA%92%E6%80%A7/10758528)大大提高。



### 对象的应用

**对象的创建和销毁都在 JavaScript 执行过程中发生，理解这种范式的含义对理解整个语言至关重要。**

#### 声明和实例化

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

#### 对象引用

在 ECMAScript 中，不能访问对象的物理表示，只能访问对象的引用。每次创建对象，存储在变量中的都是该对象的引用，而不是对象本身。

#### 对象废除

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

#### 早绑定和晚绑定

所谓绑定（binding），即把对象的接口与对象实例结合在一起的方法。

早绑定（early binding）是指在实例化对象之前定义它的属性和方法，这样编译器或解释程序就能够提前转换机器代码。在 Java 和 Visual Basic 这样的语言中，有了早绑定，就可以在开发环境中使用 IntelliSense（即给开发者提供对象中属性和方法列表的功能）。ECMAScript 不是强类型语言，所以不支持早绑定。

另一方面，晚绑定（late binding）指的是编译器或解释程序在运行前，不知道对象的类型。使用晚绑定，无需检查对象的类型，只需检查对象是否支持属性和方法即可。ECMAScript 中的所有变量都采用晚绑定方法。这样就允许执行大量的对象操作，而无任何惩罚。



### 对象类型



在 ECMAScript 中, 所有对象并非同等创建的.

一般来说, 可以创建并使用的对象有三种, **本地对象**, **内置对象**和**宿主对象**.

------

#### 本地对象

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

#### 内置对象

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

#### 宿主对象

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

#### 公用、私有和受保护作用域

#### 概念

在传统的面向对象程序设计中，主要关注于公用和私有作用域。公用作用域中的对象属性可以从对象外部访问，即开发者创建对象的实例后，就可使用它的公用属性。而私有作用域中的属性只能在对象内部访问，即对于外部世界来说，这些属性并不存在。这意味着如果类定义了私有属性和方法，则它的子类也不能访问这些属性和方法。

受保护作用域也是用于定义私有的属性和方法，只是这些属性和方法还能被其子类访问。

#### ECMAScript 只有公用作用域

对 ECMAScript 讨论上面这些作用域几乎毫无意义，因为 ECMAScript 中只存在一种作用域 - 公用作用域。ECMAScript 中的所有对象的所有属性和方法都是公用的。因此，定义自己的类和对象时，必须格外小心。记住，所有属性和方法默认都是公用的！

#### 建议性的解决方法

许多开发者都在网上提出了有效的属性作用域模式，解决了 ECMAScript 的这种问题。

由于缺少私有作用域，开发者确定了一个规约，说明哪些属性和方法应该被看做私有的。这种规约规定在属性前后加下划线：

```
obj._color_ = "blue";
```

这段代码中，属性 color 是私有的。注意，下划线并不改变属性是公用属性的事实，它只是告诉其他开发者，应该把该属性看作私有的。

有些开发者还喜欢用单下划线说明私有成员，例如：obj._color。

### 静态作用域

静态作用域定义的属性和方法任何时候都能从同一位置访问。在 Java 中，类可具有属性和方法，无需实例化该类的对象，即可访问这些属性和方法，例如 java.net.URLEncoder 类，它的函数 encode() 就是静态方法。

#### ECMAScript 没有静态作用域

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

#### 原始的方式:

因为对象的属性可以在对象创建后动态定义, 所以许多开发者都在开发JavaScript代码时编写类似下面的代码:

```javascript
 var car = new Object();
 car.color="blue";
 car.doors=4;
 car.mpg=25;
 car.showColor=function(){
     document.write(car.color);
 };

 car.showColor();
```

在上面的代码中，创建对象 car。然后给它设置几个属性：它的颜色是蓝色，有四个门，每加仑油可以跑 25 英里。最后一个属性实际上是指向函数的指针，意味着该属性是个方法。执行这段代码后，就可以使用对象 car。

不过这里有一个问题，就是可能需要创建多个 car 的实例。

[示例](define_object.html)

#### 工厂方式:

要解决该问题, 开发者创建了能创建并返回特定类型的对象的工厂函数(factory function).

例如: 函数createCar()可用于封装前面列出的创建car对象的操作:

```javascript
function createCar(){
    var car = new Object();
    car.color="blue";
    car.doors=4;
    car.mpg=25;
    car.showColor= function(){
        document.writeln(car.color)
    };

    return car;
};

var car1=createCar();
var car2=createCar();
car1.showColor();
document.writeln("<br />");
car2.showColor();
```

在这里，第一个例子中的所有代码都包含在 createCar() 函数中。此外，还有一行额外的代码，返回 car 对象（car）作为函数值。调用此函数，将创建新对象，并赋予它所有必要的属性，复制出一个我们在前面说明过的 car 对象。因此，通过这种方法，我们可以很容易地创建 car 对象的两个版本（oCar1 和 oCar2），它们的属性完全一样。

[示例](factory_function_noparameter.html)

#### 为函数传递参数

我们还可以修改 createCar() 函数，给它传递各个属性的默认值，而不是简单地赋予属性默认值：

```javascript
function createCar(color, doors, mpg){
    var car = new Object();
    car.color=color;
    car.doors=doors;
    car.mpg=mpg;
    car.showColor= function(){
        document.writeln(car.color)
    };

    return car;
};

var car1=createCar("blue", 4, 23);
var car2=createCar("red", 3, 25);
car1.showColor();
document.writeln("<br />");
car2.showColor();
```

给 createCar() 函数加上参数，即可为要创建的 car 对象的 color、doors 和 mpg 属性赋值。这使两个对象具有相同的属性，却有不同的属性值.

[示例](factory_function_with_parameter.html)

#### 在工厂函数外定义对象的方法

虽然 ECMAScript 越来越正式化，但创建对象的方法却被置之不理，且其规范化至今还遭人反对。一部分是语义上的原因（它看起来不像使用带有构造函数 new 运算符那么正规），一部分是功能上的原因。功能原因在于用这种方式必须创建对象的方法。前面的例子中，每次调用函数 createCar()，都要创建新函数 showColor()，意味着每个对象都有自己的 showColor() 版本。而事实上，每个对象都共享同一个函数。

有些开发者在工厂函数外定义对象的方法，然后通过属性指向该方法，从而避免这个问题：

```javascript
function showColor(){
    document.writeln(this.color);
};

function createCar(color, doors, mpg){
    var car = new Object();
    car.color=color;
    car.doors=doors;
    car.mpg=mpg;
    car.showColor= showColor;

    return car;
};

var car1=createCar("blue", 4, 23);
var car2=createCar("red", 3, 25);
car1.showColor();
document.writeln("<br />");
car2.showColor();
```

在上面这段重写的代码中，在函数 createCar() 之前定义了函数 showColor()。在 createCar() 内部，赋予对象一个指向已经存在的 showColor() 函数的指针。从功能上讲，这样解决了重复创建函数对象的问题；但是从语义上讲，该函数不太像是对象的方法。

所有这些问题都引发了*开发者定义*的构造函数的出现。

[示例](factory_function_with_parameter_share.html)

#### 构造函数方式

创建构造函数就像创建工厂函数一样容易。第一步选择类名，即构造函数的名字。根据惯例，这个名字的首字母大写，以使它与首字母通常是小写的变量名分开。除了这点不同，构造函数看起来很像工厂函数。请考虑下面的例子：

```javascript
function Car(color, doors, mpg){
    this.color=color;
    this.doors=doors;
    this.mpg=mpg;
    this.showColor= function () {
        document.writeln(this.color);
    };
};

var car1= new Car("blue", 4, 23);
var car2= new Car("red", 3, 25);
car1.showColor();
document.writeln("<br />");
car2.showColor();
```

下面为您解释上面的代码与工厂方式的差别。首先在构造函数内没有创建对象，而是使用 this 关键字。使用 new 运算符构造函数时，在执行第一行代码前先创建一个对象，只有用 this 才能访问该对象。然后可以直接赋予 this 属性，默认情况下是构造函数的返回值（不必明确使用 return 运算符）。

现在，用 new 运算符和类名 Car 创建对象，就更像 ECMAScript 中一般对象的创建方式了。

[示例](constructed_function.html)

你也许会问，这种方式在管理函数方面是否存在于前一种方式相同的问题呢？是的。

就像工厂函数，构造函数会重复生成函数，为每个对象都创建独立的函数版本。不过，与工厂函数相似，也可以用外部函数重写构造函数，同样地，这么做语义上无任何意义。这正是下面要讲的原型方式的优势所在。

#### 原型方式

该方式利用了对象的 prototype 属性，可以把它看成创建新对象所依赖的原型。

这里，首先用空构造函数来设置类名。然后所有的属性和方法都被直接赋予 prototype 属性。我们重写了前面的例子，代码如下：

```javascript
function Car(){};

Car.prototype.color="blue";
Car.prototype.doors=4;
Car.prototype.mpg=25;
Car.prototype.showColor = function () {
    document.writeln(this.color);
};

var car1= new Car();
var car2 = new Car();
car1.showColor();
document.writeln("<br />");
car2.showColor();
```

在这段代码中，首先定义构造函数（Car），其中无任何代码。接下来的几行代码，通过给 Car 的 prototype 属性添加属性去定义 Car 对象的属性。调用 new Car() 时，原型的所有属性都被立即赋予要创建的对象，意味着所有 Car 实例存放的都是指向 showColor() 函数的指针。从语义上讲，所有属性看起来都属于一个对象，因此解决了前面两种方式存在的问题。

此外，使用这种方式，还能用 instanceof 运算符检查给定变量指向的对象的类型。因此，下面的代码将输出 TRUE：

```javascript
document.writeln(car1 instanceof Car);
```

#### 原型方式的问题

原型方式看起来是个不错的解决方案。遗憾的是，它并不尽如人意。

首先，这个构造函数没有参数。使用原型方式，不能通过给构造函数传递参数来初始化属性的值，因为 Car1 和 Car2 的 color 属性都等于 "blue"，doors 属性都等于 4，mpg 属性都等于 25。这意味着必须在对象创建后才能改变属性的默认值，这点很令人讨厌，但还没完。真正的问题出现在属性指向的是对象，而不是函数。函数共享不会造成问题，但对象却很少被多个实例共享。请思考下面的例子：

```javascript

function Car(){};

Car.prototype.color="blue";
Car.prototype.doors=4;
Car.prototype.mpg=25;
Car.prototype.drivers = new Array("Mike", "John");
Car.prototype.showColor = function () {
    document.writeln(this.color);
};

var car1= new Car();
var car2 = new Car();
car1.showColor();
document.writeln("<br />");
car2.showColor();
document.writeln("<br />");
document.writeln(car1 instanceof Car);
document.writeln("<br />");
document.writeln(car2 instanceof Car);

car1.drivers.push("Bill");
document.writeln("<br />");
document.writeln("car1's drivers: "+car1.drivers);

document.writeln("<br />");
document.writeln("car2's drivers: "+car2.drivers);
```

上面的代码中，属性 drivers 是指向 Array 对象的指针，该数组中包含两个名字 "Mike" 和 "John"。由于 drivers 是引用值，Car 的两个实例都指向同一个数组。这意味着给 oCar1.drivers 添加值 "Bill"，在 oCar2.drivers 中也能看到。输出这两个指针中的任何一个，结果都是显示字符串 "Mike,John,Bill"。

由于创建对象时有这么多问题，你一定会想，是否有种合理的创建对象的方法呢？答案是有，需要联合使用构造函数和原型方式。

[示例](prototype_function_with_reference_types.html)

#### 混合的构造函数/原型方式

联合使用构造函数和原型方式，就可像用其他程序设计语言一样创建对象。这种概念非常简单，即用构造函数定义对象的所有非函数属性，用原型方式定义对象的函数属性（方法）。结果是，所有函数都只创建一次，而每个对象都具有自己的对象属性实例。

我们重写了前面的例子，代码如下：

```javascript
function Car(color, doors, mpg){
    this.color=color;
    this.doors=doors;
    this.mpg=mpg;
    this.drivers= new Array("Mike", "John");
};

Car.prototype.showColor = function () {
    document.writeln(this.color);
};


var car1= new Car("Blue", 3, 23);
var car2 = new Car("Red", 4, 25);
car1.showColor();
document.writeln("<br />");
car2.showColor();
document.writeln("<br />");
document.writeln(car1 instanceof Car);
document.writeln("<br />");
document.writeln(car2 instanceof Car);

car1.drivers.push("Bill");
document.writeln("<br />");
document.writeln("car1's drivers: "+car1.drivers);

document.writeln("<br />");
document.writeln("car2's drivers: "+car2.drivers);
```

现在就更像创建一般对象了。所有的非函数属性都在构造函数中创建，意味着又能够用构造函数的参数赋予属性默认值了。因为只创建 showColor() 函数的一个实例，所以没有内存浪费。此外，给 oCar1 的 drivers 数组添加 "Bill" 值，不会影响到 oCar2 的数组，所以输出这些数组的值时，oCar1.drivers 显示的是 "Mike,John,Bill"，而 oCar2.drivers 显示的是 "Mike,John"。因为使用了原型方式，所以仍然能利用 instanceof 运算符来判断对象的类型。

这种方式是 ECMAScript 采用的主要方式，它具有其他方式的特性，却没有他们的副作用。不过，有些开发者仍觉得这种方法不够完美。

#### 动态原型方法

对于习惯使用其他语言的开发者来说，使用混合的构造函数/原型方式感觉不那么和谐。毕竟，定义类时，大多数面向对象语言都对属性和方法进行了视觉上的封装。请考虑下面的 Java 类：

```java
class Car {
  public String color = "blue";
  public int doors = 4;
  public int mpg = 25;

  public Car(String color, int doors, int mpg) {
    this.color = color;
    this.doors = doors;
    this.mpg = mpg;
  }
  
  public void showColor() {
    System.out.println(color);
  }
}
```

Java 很好地打包了 Car 类的所有属性和方法，因此看见这段代码就知道它要实现什么功能，它定义了一个对象的信息。批评混合的构造函数/原型方式的人认为，在构造函数内部找属性，在其外部找方法的做法不合逻辑。因此，他们设计了动态原型方法，以提供更友好的编码风格。

动态原型方法的基本想法与混合的构造函数/原型方式相同，即在构造函数内定义非函数属性，而函数属性则利用原型属性定义。唯一的区别是赋予对象方法的位置。下面是用动态原型方法重写的 Car 类：

```javascript
function Car(color, doors, mpg){
    this.color=color;
    this.doors=doors;
    this.mpg=mpg;
    this.drivers= new Array("Mike", "John");

    if(typeof Car._initialized == "undefined"){
        Car.prototype.showColor= function () {
            document.writeln(this.color);
        };
    };

    Car._initialized = true;
};
```

直到检查 typeof Car._initialized 是否等于 "undefined" 之前，这个构造函数都未发生变化。这行代码是动态原型方法中最重要的部分。如果这个值未定义，构造函数将用原型方式继续定义对象的方法，然后把 Car._initialized 设置为 true。如果这个值定义了（它的值为 true 时，typeof 的值为 Boolean），那么就不再创建该方法。简而言之，该方法使用标志（_initialized）来判断是否已给原型赋予了任何方法。该方法只创建并赋值一次，传统的 OOP 开发者会高兴地发现，这段代码看起来更像其他语言中的类定义了。

[示例](dynamic_prototype_function.html)

#### 采用哪种方式

如前所述，目前使用最广泛的是混合的构造函数/原型方式。此外，动态原始方法也很流行，在功能上与构造函数/原型方式等价。可以采用这两种方式中的任何一种。不过不要单独使用经典的构造函数或原型方式，因为这样会给代码引入问题。

------

### 修改对象

**通过使用ECMAScript, 不仅可以创建对象, 还可以修改已有对象的行为.**

**prototype属性不仅可以定义构造函数的属性和方法, 还可以为本地对象添加属性和方法**.

#### 创建新方法

可以用prototype属性为任何已有的类定义新方法, 就像处理自己的类一样. 例如, 还记得Number类的toString()方法吗? 如果给它传递参数16, 它将输出16进制的字符串.如果这个方法的参数是 2，那么它将输出二进制的字符串。我们可以创建一个方法，可以把数字对象直接转换为十六进制字符串。创建这个方法非常简单：

```javascript
Number.prototype.toHexString = function () {
    return this.toString(16);
};

var num = 15;
document.writeln(num.toHexString());
```

由于数字 15 等于十六进制中的 F，因此将显示 "F"。

[示例](function.html)

#### 重命名已有方法

我们还可以为已有的方法命名更易懂的名称。例如，可以给 Array 类添加两个方法 enqueue() 和 dequeue()，只让它们反复调用已有的 push() 和 shift() 方法即可：

```javascript
Array.prototype.enqueue = function (item) {
    this.push(item);
};

Array.prototype.dequeue = function (item) {
    this.shift(item);
};
```

#### 添加与已有方法无关的方法

当然，还可以添加与已有方法无关的方法。例如，假设要判断某个项在数组中的位置，没有本地方法可以做这种事情。我们可以轻松地创建下面的方法：

```javascript
Array.prototype.indexOf = function (item) {
    for (var i=0; i<this.length; i++) {
        if (item == this[i]) {
            return i;
        }
    }

    return -1;
}
```

该方法 indexOf() 与 String 类的同名方法保持一致，在数组中检索每个项，直到发现与传进来的项相同的项目为止。如果找到相同的项，则返回该项的位置，否则，返回 -1。有了这种定义，我们可以编写下面的代码：

```javascript
var arr = new Array(3)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"

document.writeln("Thomas's index is :"+arr.indexOf("Thomas"))
```

#### 为本地对象添加新方法

最后，如果想给 ECMAScript 中每个本地对象添加新方法，必须在 Object 对象的 prototype 属性上定义它。前面的章节我们讲过，所有本地对象都继承了 Object 对象，所以对 Object 对象做任何改变，都会反应在所有本地对象上。例如，如果想添加一个用警告输出对象的当前值的方法，可以采用下面的代码：

```javascript
Object.prototype.showValue = function () {
    alert(this.valueOf());
};

var str = "hello";
var num = 25;
str.showValue();
num.showValue();
```

这里，String 和 Number 对象都从 Object 对象继承了 showValue() 方法，分别在它们的对象上调用该方法，将显示 "hello" 和 "25"。

#### 重定义已有方法

就像能给已有的类定义新方法一样，也可重定义已有的方法。如前面的章节所述，函数名只是指向函数的指针，因此可以轻松地指向其他函数。如果修改了本地方法，如 toString()，会出现什么情况呢？

```javascript
Function.prototype.toString = function () {
    return "Function code hidden";
};

function demo() {
    doucment.writeln("Hello World!");
}

document.write("<br />")
document.writeln(demo.toString());
```

前面的代码完全合法，运行结果完全符合预期：

```
Function code hidden
```

 Function 的 toString() 方法通常输出的是函数的源代码。覆盖该方法，可以返回另一个字符串（在这个例子中，可以返回 "Function code hidden"）。不过，toString() 指向的原始函数怎么了呢？它将被无用存储单元回收程序回收，因为它被完全废弃了。没有能够恢复原始函数的方法，所以在覆盖原始方法前，比较安全的做法是存储它的指针，以便以后的使用。有时你甚至可能在新方法中调用原始方法：

```javascript
Function.prototype.originalToString = Function.prototype.toString;

Function.prototype.toString = function () {
    var functionStrValue= this.originalToString();
    if(functionStrValue.length > 100){
        return "Function too long to display.";
    } else {
        return functionStrValue;
    };
};

function demo() {
    doucment.writeln("Hello World!");
}

function demo2() {
    doucment.writeln("Hello World! a b c d e f g Hello World! a b c d e f g Hello World! a b c d e f g Hello World! a b c d e f g Hello World! a b c d e f g Hello World! a b c d e f g Hello World! a b c d e f g Hello World! a b c d e f g Hello World! a b c d e f g Hello World! a b c d e f g");
}

document.write("<br />")
document.writeln(demo.toString());
document.write("<br />")
document.writeln(demo2.toString());
```

在这段代码中，第一行代码把对当前 toString() 方法的引用保存在属性 originalToString 中。然后用定制的方法覆盖了 toString() 方法。新方法将检查该函数源代码的长度是否大于 100。如果是，就返回错误信息，说明该函数代码太长，否则调用 originalToString() 方法，返回函数的源代码。

#### 极晚绑定(Very Late Binding)

从技术上讲，根本不存在极晚绑定。本书采用该术语描述 ECMAScript 中的一种现象，即能够在对象实例化后再定义它的方法。例如：

```javascript
var obj = new Object();
Object.prototype.helloWorld = function () {
    document.writeln("Hello World!");
};

obj.helloWorld();
```

在大多数程序设计语言中，必须在实例化对象之前定义对象的方法。这里，方法 helloWorld() 是在创建 Object 类的一个实例之后来添加进来的。在传统语言中不仅没听说过这种操作，也没听说过该方法还会自动赋予 Object 对象的实例并能立即使用（接下来的一行）。

> Note
>
> **注意：不建议使用极晚绑定方法，因为很难对其跟踪和记录。不过，还是应该了解这种可能**。
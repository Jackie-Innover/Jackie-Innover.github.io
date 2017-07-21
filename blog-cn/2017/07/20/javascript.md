# JavaScript

> Note
>
> - 对大小写敏感
>
> - JavaScript会忽略多余的空格. 可以使用空格来提高代码可读性.
>
> - 在文本字符串中可以使用反斜杠对代码进行换行
>
> - JavaScript是脚本语言, 浏览器会在读取代码时, 逐行的执行脚本代码.
>
> - 重新声明变量, 改变量原来的值不会丢失.
>
>   在以下两条语句执行后, 变量carname的值依然是 "Volvo"
>
>   ```
>   var carname="Volvo";
>   var carname;
>   ```
>
> - 可以在字符串中使用单引号或双引号, 只要不匹配包围字符串的引号即可.
>
>   ```
>   var answer="Nice to meet you!";
>   var answer="He is called 'Bill'";
>   var answer='He is called "Bill"';
>   ```
>
> - 极大或极小的数字可以通过科学(指数)计数法来书写.
>
>   ```
>   var y=123e5;      // 12300000
>   var z=123e-5;     // 0.00123
>   ```
>
> - 布尔类型只有两个值: true 或 false.
>
> - JavaScript 数组
>
>   ```
>   var cars = new Array();
>   cars[0] = "Audi";
>   cars[1] = "BMW";
>   cars[2] = "Volvo";
>   ```
>
>   condensed array:
>
>   ```
>   var cars = new Array("Audi", "BMW", "Volvo");
>   ```
>
>   literal array:
>
>   ```
>   var cars = ["Audi", "BMW", "Volvo"];
>   ```
>
> - JavaScript 对象
>
>   对象由大括号分隔. 在括号内部, 对象的属性以名称和值的形式 (name : value) 来定义. 属性由逗号分隔.
>
>   ```
>   var person = {firstName : "Bill", lastName : "Gates", id : 5566};
>   ```
>
>   上面的示例中的person对象有三个属性: firstName, lastName 以及 id.
>
>   空格和折行无关紧要, 声明可以横跨多行:
>
>   ```
>   var person = {
>   firstName : "Bill", 
>   lastName : "Gates", 
>   id : 5566
>   };
>   ```
>
>   ```
>   var person = new Object;
>   person.firstName = "Bill";
>   person.lastName = "Gates";
>   person.id = 5566;
>   ```
>
>   可以向已存在的对象添加属性和方法.
>
>   ```
>   person.age = 56;
>   person.eyeColor = "blue";
>   ```
>
>   对象属性有两种寻址方式: 
>
>   ```
>   name = person.firstName;
>   name = person["firstName"];
>   ```
>
>
> - Undefined 和 Null
>
>   Undefined 这个值表示变量不含有值.
>
>   可以通过将变量的值设置为null 来清空变量.
>
>   ```
>   cars = null;
>   person = null;
>   ```
>
> - 声明变量类型
>
>   当声明新变量时, 可以使用关键字 "new" 来指定变量类型:
>
>   ```
>   var carName = new String;
>   var x = new Number;
>   var y = new Boolean;
>   var cars = new Array;
>   var person = new Object;
>   ```
>
>   JavaScript变量均为对象. 当声明一个变量时, 就创建了一个新的对象. 对象是拥有属性和方法的数据.
>
> - 函数语法
>
>   函数就是包裹在大括号中的代码块, 前面使用了关键字 function:
>
>   ```
>   function sayHello(){
>     // 代码块
>   }
>   ```
>
>   当调用该函数时, 会执行函数内的代码.
>
>   **带参数的函数**:
>
>   ```
>   function sayHello(name, job){
>     // 代码块
>   }
>   ```
>
>   **带返回值的函数**:
>
>   使用return语句返回值.
>
>   如果仅仅希望退出函数时, 也可使用return语句. 返回值是可选的.
>
>   ```
>   function add(x, y){
>     return x+y;
>   }
>   ```
>
> - 局部变量
>
>   在JavaScript函数内部声明的变量是局部变量, 所以只能在函数内部访问它. 改变量的作用于是局部的.
>
>   可以在不同的函数中使用名称相同的局部变量. 因为只有声明过该变量的函数才能识别出该变量.
>
>   只要函数运行完成, 本地变量就会被删除.
>
> - 全局变量
>
>   在函数外声明的变量是全局变量, 网页上的所有脚本和函数都能访问它.
>
> - 变量的生命周期
>
>   变量的生命周期从它们被声明的时间开始.
>
>   局部变量会在函数运行完成以后被删除.
>
>   全局变量会在页面关闭后被删除.
>
> - **向未声明的变量分配值**
>
>   如果您把值赋给尚未声明的变量, 该变量将自动作为全局变量声明.
>
>   ```
>   carName = "Volvo";
>   ```
>
>   将声明一个全局变量carName, 即使它在函数内执行.
>
> - 如果把数字与字符串相加,会自动把数字转换为字符串,  结果将成为字符串.
>
> - == & ===
>
>   给定 x = 5, 下面的表格解释:
>
>   | 运算符  | 描述   | 例子                           |
>   | :--- | :--- | :--------------------------- |
>   | ==   | 等于   | x==8                         |
>   | ===  | 全等   | x===5 为true, x==="5" 为 false |
>
> - JavaScript标签
>
>   如需标记 JavaScript语句, 请在语句之前加上冒号:
>
>   ```
>   label:
>   语句
>   ```
>
>   break 和 continue语句仅仅是能够跳出代码块的语句.
>
>   语法:
>
>   ```
>   break labelName;
>   continue labelName;
>   ```
>
>   continue 语句(带有或不带有标签引用) 只能用在循环中.
>
>   break 语句 (不带标签引用), 只能用在循环或Switch中.
>
>   通过标签引用, break语句可用于跳出任何JavaScript代码块.
>
> - 改变HTML输出流 
>
>   document.write("demo");
>
>   ```
>   <!DOCTYPE html>
>   <html>
>   <body>
>
>   <script>
>   document.write(Date());
>   </script>
>
>   </body>
>   </html>
>   ```
>
> - 改变HTML内容
>
>   document.getElementById(id).innerHTML="";
>
>   ```
>   <!DOCTYPE html>
>   <html>
>   <body>
>
>   <h1 id="header">Old Header</h1>
>
>   <script>
>   var element=document.getElementById("header");
>   element.innerHTML="New Header";
>   </script>
>
>   </body>
>   </html>
>   ```
>
>   例子解释：
>
>   - 上面的 HTML 文档含有 id="header" 的 <h1> 元素
>   - 我们使用 HTML DOM 来获得 id="header" 的元素
>   - JavaScript 更改此元素的内容 (innerHTML)
>
> - 改变HTML属性
>
>   document.getElementById(id).attribute=new value;
>
>   ```
>   <!DOCTYPE html>
>   <html>
>   <body>
>
>   <img id="image" src="smiley.gif">
>
>   <script>
>   document.getElementById("image").src="landscape.jpg";
>   </script>
>
>   </body>
>   </html>
>   ```
>
>   例子解释:
>
>   - 上面的 HTML 文档含有 id="image" 的 <img> 元素
>   - 我们使用 HTML DOM 来获得 id="image" 的元素
>   - JavaScript 更改此元素的属性（把 "smiley.gif" 改为 "landscape.jpg"）
>
> - 改变HTML样式
>
>   如需改变HTML元素的样式, 请使用这个语法:
>
>   ```
>   <p id="p2">Hello World!</p>
>
>   <script>
>   document.getElementById("p2").style.color="blue";
>   </script>
>   ```
>
>   [Demo](changestyle.html)
>
>   [HTML DOM Style对象](http://www.w3school.com.cn/jsref/dom_obj_style.asp)
>
> - JavaScript HTML DOM 事件
>
>   HTML DOM使JavaScript有能力对HTML事件做出反应
>
>   ​
>
> - aa



> JavaScript注释
>
> 单行注释: //
>
> 多行注释: /*       */



> JavaScript错误 -  Throw, Try 和 Catch
>
> try 语句测试代码块的错误
>
> catch 语句处理错误
>
> throw 语句创建自定义错误
>
> 
>
> 当JavaScript 引擎执行JavaScript代码时, 会发生各种错误:
>
> - 可能是语法错误，通常是程序员造成的编码错误或错别字。
> - 可能是拼写错误或语言中缺少的功能（可能由于浏览器差异）。
> - 可能是由于来自服务器或用户的错误输出而导致的错误。
> - 当然，也可能是由于许多其他不可预知的因素。
>
> JavaScript抛出错误
>
> 当错误发生时，当事情出问题时，JavaScript 引擎通常会停止，并生成一个错误消息。
>
> 描述这种情况的技术术语是：JavaScript 将***抛出***一个错误。
>
> ## JavaScript 测试和捕捉
>
> *try* 语句允许我们定义在执行时进行错误测试的代码块。
>
> *catch* 语句允许我们定义当 try 代码块发生错误时，所执行的代码块。
>
> JavaScript 语句 *try* 和 *catch* 是成对出现的。
>
> ```
> try
>   {
>   //在这里运行代码
>   }
> catch(err)
>   {
>   //在这里处理错误
>   }
> ```
>
> ### 实例
>
> 在下面的例子中，我们故意在 try 块的代码中写了一个错字。
>
> catch 块会捕捉到 try 块中的错误，并执行代码来处理它。
>
> ## Throw 语句
>
> throw 语句允许我们创建自定义错误。
>
> 正确的技术术语是：创建或*抛出异常*（exception）。
>
> 如果把 throw 与 try 和 catch 一起使用，那么您能够控制程序流，并生成自定义的错误消息。
>
> ```
> throw exception
> ```
>
> 异常可以是 JavaScript 字符串、数字、逻辑值或对象。
> 实例
> 本例检测输入变量的值。如果值是错误的，会抛出一个异常（错误）。catch 会捕捉到这个错误，并显示一段自定义的错误消息：
>
> ```
> <script>
> function myFunction()
> {
> try
>   {
>   var x=document.getElementById("demo").value;
>   if(x=="")    throw "empty";
>   if(isNaN(x)) throw "not a number";
>   if(x>10)     throw "too high";
>   if(x<5)      throw "too low";
>   }
> catch(err)
>   {
>   var y=document.getElementById("mess");
>   y.innerHTML="Error: " + err + ".";
>   }
> }
> </script>
>
> <h1>My First JavaScript</h1>
> <p>Please input a number between 5 and 10:</p>
> <input id="demo" type="text">
> <button type="button" onclick="myFunction()">Test Input</button>
> <p id="mess"></p>
> ```
>
> zzz






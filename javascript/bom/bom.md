# 浏览器对象模型 

[TOC]

BOM (Browser Object Model) 

**浏览器对象模型 (BOM) 使 JavaScript 有能力与浏览器“对话”。**

浏览器对象模型（Browser Object Model）尚无正式标准。

# Window

## Window 对象

Window对象表示当前浏览器的窗口，是JavaScript的顶级对象，我们创建的所有对象、函数、变量都是Window对象的成员。

不过，一般情况下我们的代码中省略了window对象，浏览器默认会作为window对象的成员来调用。

![object_model](/images/object_model.png)

所有浏览器都支持 *window* 对象。它表示浏览器窗口。

所有 JavaScript 全局对象、函数以及变量均自动成为 window 对象的成员。

全局变量是 window 对象的属性。

全局函数是 window 对象的方法。

甚至 HTML DOM 的 document 也是 window 对象的属性之一：

```javascript
window.document.getElementById("header");
```

与此相同：

```javascript
document.getElementById("header");
```

## Window 尺寸

有三种方法能够确定浏览器窗口的尺寸（浏览器的视口，不包括工具栏和滚动条）。

对于Internet Explorer、Chrome、Firefox、Opera 以及 Safari：

- window.innerHeight - 浏览器窗口的内部高度
- window.innerWidth - 浏览器窗口的内部宽度

对于 Internet Explorer 8、7、6、5：

- document.documentElement.clientHeight
- document.documentElement.clientWidth

或者

- document.body.clientHeight
- document.body.clientWidth

实用的 JavaScript 方案（涵盖所有浏览器）：

### 实例

```javascript
var w=window.innerWidth
|| document.documentElement.clientWidth
|| document.body.clientWidth;

var h=window.innerHeight
|| document.documentElement.clientHeight
|| document.body.clientHeight;
```

[亲自试一试](window_width_height.html)

该例显示浏览器窗口的高度和宽度：（不包括工具栏/滚动条）

## 其他 Window 方法

一些其他方法：

- window.open() - 打开新窗口
- window.close() - 关闭当前窗口
- window.moveTo() - 移动当前窗口
- window.resizeTo() - 调整当前窗口的尺寸



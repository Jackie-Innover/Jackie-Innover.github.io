# AJAX

**AJAX**即“**Asynchronous JavaScript and XML**”（异步的[JavaScript](https://zh.wikipedia.org/wiki/JavaScript)与[XML](https://zh.wikipedia.org/wiki/XML)技术），指的是一套综合了多项技术的[浏览器](https://zh.wikipedia.org/wiki/%E7%80%8F%E8%A6%BD%E5%99%A8)端[网页](https://zh.wikipedia.org/wiki/%E7%B6%B2%E9%A0%81)开发技术。Ajax的概念由[杰西·詹姆士·贾瑞特](https://zh.wikipedia.org/wiki/%E5%82%91%E8%A5%BF%C2%B7%E8%A9%B9%E5%A7%86%E5%A3%AB%C2%B7%E8%B3%88%E7%91%9E%E7%89%B9)所提出[[1\]](https://zh.wikipedia.org/wiki/AJAX#cite_note-1)。

传统的Web应用允许用户端填写表单（form），当提交表单时就向[网页服务器](https://zh.wikipedia.org/wiki/%E7%B6%B2%E9%A0%81%E4%BC%BA%E6%9C%8D%E5%99%A8)发送一个请求。服务器接收并处理传来的表单，然后送回一个新的网页，但这个做法浪费了许多带宽，因为在前后两个页面中的大部分HTML码往往是相同的。由于每次应用的沟通都需要向服务器发送请求，应用的回应时间依赖于服务器的回应时间。这导致了用户界面的回应比本机应用慢得多。

与此不同，AJAX应用可以仅向服务器发送并取回必须的数据，并在客户端采用JavaScript处理来自服务器的回应。因为在服务器和浏览器之间交换的数据大量减少（大约只有原来的5%）[[来源请求\]](https://zh.wikipedia.org/wiki/Wikipedia:%E5%88%97%E6%98%8E%E6%9D%A5%E6%BA%90),服务器回应更快了。同时，很多的处理工作可以在发出请求的[客户端](https://zh.wikipedia.org/wiki/%E5%AE%A2%E6%88%B7%E7%AB%AF)机器上完成，因此Web服务器的负荷也减少了。

类似于[DHTML](https://zh.wikipedia.org/wiki/DHTML)或[LAMP](https://zh.wikipedia.org/wiki/LAMP)，AJAX不是指一种单一的技术，而是有机地利用了一系列相关的技术。虽然其名称包含XML，但实际上数据格式可以由[JSON](https://zh.wikipedia.org/wiki/JSON)代替，进一步减少数据量，形成所谓的AJAJ。而客户端与服务器也并不需要异步。一些基于AJAX的“派生／合成”式（derivative/composite）的技术也正在出现，如[AFLAX](https://zh.wikipedia.org/wiki/AFLAX)。



## 应用[[编辑](https://zh.wikipedia.org/w/index.php?title=AJAX&action=edit&section=1)]

- 运用[XHTML](https://zh.wikipedia.org/wiki/XHTML)+[CSS](https://zh.wikipedia.org/wiki/CSS)来表达信息；
- 运用[JavaScript](https://zh.wikipedia.org/wiki/JavaScript)操作[DOM](https://zh.wikipedia.org/wiki/%E6%96%87%E4%BB%B6%E7%89%A9%E4%BB%B6%E6%A8%A1%E5%9E%8B)（Document Object Model）来运行动态效果；
- 运用[XML](https://zh.wikipedia.org/wiki/XML)和[XSLT](https://zh.wikipedia.org/wiki/XSLT)操作数据
- 运用[XMLHttpRequest](https://zh.wikipedia.org/wiki/XMLHttpRequest)或新的Fetch API与[网页服务器](https://zh.wikipedia.org/wiki/%E7%B6%B2%E9%A0%81%E4%BC%BA%E6%9C%8D%E5%99%A8)进行异步数据交换；
- 注意：AJAX与[Flash](https://zh.wikipedia.org/wiki/Adobe_Flash_Player)、[Silverlight](https://zh.wikipedia.org/wiki/Silverlight)和[Java Applet](https://zh.wikipedia.org/wiki/Java_Applet)等[RIA](https://zh.wikipedia.org/wiki/%E4%B8%B0%E5%AF%8C%E4%BA%92%E8%81%94%E7%BD%91%E5%BA%94%E7%94%A8%E7%A8%8B%E5%BA%8F)技术是有区分的。



## 发展史[[编辑](https://zh.wikipedia.org/w/index.php?title=AJAX&action=edit&section=2)]

上个世纪90年代，几乎所有的网站都由HTML页面实现，服务器处理每一个用户请求都需要重新加载网页。这样的处理方式效率不高。用户的体验是所有页面都会消失，再重新载入，即使只是一部分页面元素改变也要重新载入整个页面，不仅要刷新改变的部分，连没有变化的部分也要刷新。这会加重服务器的负担。

这可以用[异步](https://zh.wikipedia.org/w/index.php?title=%E5%BC%82%E6%AD%A5&action=edit&redlink=1)加载来解决。1995年，JAVA语言的第一版发布，随之发布的的Java applets（JAVA小程序）首次实现了异步加载。浏览器通过运行嵌入网页中的Java applets与服务器交换数据，不必刷新网页。1996年，Internet Explorer将iframe元素加入到HTML，支持局部刷新网页。

1998年前后，Outlook Web Access小组写成了允许[客户端脚本](https://zh.wikipedia.org/w/index.php?title=%E5%AE%A2%E6%88%B7%E7%AB%AF%E8%84%9A%E6%9C%AC&action=edit&redlink=1)发送HTTP请求（[XMLHTTP](https://zh.wikipedia.org/wiki/XMLHTTP)）的第一个组件。该组件原属于微软Exchange Server，并且迅速地成为了Internet Explorer 4.0[[2\]](https://zh.wikipedia.org/wiki/AJAX#cite_note-2)的一部分。部分观察家认为，Outlook Web Access是第一个应用了Ajax技术的成功的商业应用程序，并成为包括Oddpost的网络邮件产品在内的许多产品的领头羊。但是，2005年初，许多事件使得Ajax被大众所接受。[Google](https://zh.wikipedia.org/wiki/Google)在它著名的交互应用程序中使用了异步通讯，如[Google讨论组](https://zh.wikipedia.org/w/index.php?title=Google%E8%AE%A8%E8%AE%BA%E7%BB%84&action=edit&redlink=1)、[Google地图](https://zh.wikipedia.org/wiki/Google%E5%9C%B0%E5%9B%BE)、[Google搜索建议](https://zh.wikipedia.org/w/index.php?title=Google%E6%90%9C%E7%B4%A2%E5%BB%BA%E8%AE%AE&action=edit&redlink=1)、[Gmail](https://zh.wikipedia.org/wiki/Gmail)等。Ajax这个词由《*Ajax: A New Approach to Web Applications*》一文所创，该文的迅速流传提高了人们使用该项技术的意识。另外，对Mozilla/Gecko的支持使得该技术走向成熟，变得更为简单易用。



## 优缺点[[编辑](https://zh.wikipedia.org/w/index.php?title=AJAX&action=edit&section=3)]

使用Ajax的最大优点，就是能在不更新整个页面的前提下维护数据。这使得Web应用程序更为迅捷地回应用户动作，并避免了在网络上发送那些没有改变的信息。

Ajax不需要任何浏览器插件，但需要用户**允许JavaScript在浏览器上执行**。就像[DHTML](https://zh.wikipedia.org/wiki/DHTML)应用程序那样，Ajax应用程序必须在众多不同的浏览器和平台上经过严格的测试。随着Ajax的成熟，一些简化Ajax使用方法的程序库也相继问世。同样，也出现了另一种辅助程序设计的技术，为那些不支持[JavaScript](https://zh.wikipedia.org/wiki/JavaScript)的用户提供替代功能。

对应用Ajax最主要的批评就是，它可能破坏浏览器的后退与加入收藏书签功能[[3\]](https://zh.wikipedia.org/wiki/AJAX#cite_note-3)。在动态更新页面的情况下，用户无法回到前一个页面状态，这是因为浏览器仅能记下历史记录中的[静态页面](https://zh.wikipedia.org/w/index.php?title=%E9%9D%99%E6%80%81%E9%A1%B5%E9%9D%A2&action=edit&redlink=1)。一个被完整读入的页面与一个已经被动态修改过的页面之间的可能差别非常微妙；用户通常都希望单击后退按钮，就能够取消他们的前一次操作，但是在Ajax应用程序中，却无法这样做。不过开发者已想出了种种办法来解决这个问题，[HTML5](https://zh.wikipedia.org/wiki/HTML5) 之前的方法大多是在用户单击后退按钮访问历史记录时，通过创建或使用一个隐藏的IFRAME来重现页面上的变更。（例如，当用户在Google Maps中单击后退时，它在一个隐藏的[IFRAME](https://zh.wikipedia.org/w/index.php?title=IFRAME&action=edit&redlink=1)中进行搜索，然后将搜索结果反映到Ajax元素上，以便将应用程序状态恢复到当时的状态）。

关于无法将状态加入收藏或书签的问题，[HTML5](https://zh.wikipedia.org/wiki/HTML5)之前的一种方式是使用[URL](https://zh.wikipedia.org/wiki/URL)片断标识符（通常被称为[锚点](https://zh.wikipedia.org/wiki/%E9%94%9A%E7%82%B9)，即URL中#后面的部分）来保持追踪，允许用户回到指定的某个应用程序状态。（许多浏览器允许JavaScript动态更新锚点，这使得Ajax应用程序能够在更新显示内容的同时更新锚点。）[HTML5](https://zh.wikipedia.org/wiki/HTML5) 以后可以直接操作浏览历史，并以字符串形式存储网页状态，将网页加入网页收藏夹或书签时状态会被隐形地保留。上述两个方法也可以同时解决无法后退的问题。

进行Ajax开发时，网络延迟——即用户发出请求到服务器发出响应之间的间隔——需要慎重考虑。如果不给予用户明确的回应[[4\]](https://zh.wikipedia.org/wiki/AJAX#cite_note-4)，没有恰当的预读数据[[5\]](https://zh.wikipedia.org/wiki/AJAX#cite_note-5)，或者对XMLHttpRequest的不恰当处理[[6\]](https://zh.wikipedia.org/wiki/AJAX#cite_note-6)，都会使用户感到厌烦[[7\]](https://zh.wikipedia.org/wiki/AJAX#cite_note-7)。通常的解决方案是，使用一个可视化的组件来告诉用户系统正在进行后台操作并且正在读取数据和内容。



## 兼容性[[编辑](https://zh.wikipedia.org/w/index.php?title=AJAX&action=edit&section=4)]

[JavaScript](https://zh.wikipedia.org/wiki/JavaScript)编程的最大问题来自不同的浏览器对各种技术和标准的支持。

XmlHttpRequest对象在不同浏览器中不同的创建方法，以下是跨浏览器的通用方法：

```
// Provide the XMLHttpRequest class for IE 5.x-6.x:
// Other browsers (including IE 7.x-8.x) ignore this
//   when XMLHttpRequest is predefined
var xmlHttp;
if (typeof XMLHttpRequest != "undefined") {
    xmlHttp = new XMLHttpRequest();
} else if (window.ActiveXObject) {
    var aVersions = ["Msxml2.XMLHttp.5.0", "Msxml2.XMLHttp.4.0", "Msxml2.XMLHttp.3.0", "Msxml2.XMLHttp", "Microsoft.XMLHttp"];
    for (var i = 0; i < aVersions.length; i++) {
        try {
            xmlHttp = new ActiveXObject(aVersions[i]);
            break;
        } catch (e) {}
    }
}

```

AJAX支持的[浏览器](https://zh.wikipedia.org/wiki/%E6%B5%8F%E8%A7%88%E5%99%A8)有：[Internet Explorer](https://zh.wikipedia.org/wiki/Internet_Explorer)、[Chrome](https://zh.wikipedia.org/wiki/Google_Chrome)、[Firefox](https://zh.wikipedia.org/wiki/Firefox)、[Opera](https://zh.wikipedia.org/wiki/Opera%E9%9B%BB%E8%85%A6%E7%80%8F%E8%A6%BD%E5%99%A8)、[Konqueror](https://zh.wikipedia.org/wiki/Konqueror)及Mac OS的[Safari](https://zh.wikipedia.org/wiki/Safari)。但是Opera不支持[XSL格式对象](https://zh.wikipedia.org/wiki/XSL-FO)，也不支持[XSLT](https://zh.wikipedia.org/wiki/XSLT)[[8\]](https://zh.wikipedia.org/wiki/AJAX#cite_note-8)。



## 开发挑战及解决方案[[编辑](https://zh.wikipedia.org/w/index.php?title=AJAX&action=edit&section=5)]

| [![Unbalanced scales.svg](https://upload.wikimedia.org/wikipedia/commons/thumb/f/fe/Unbalanced_scales.svg/45px-Unbalanced_scales.svg.png)](https://zh.wikipedia.org/wiki/File:Unbalanced_scales.svg) | **此章节的中立性有争议。**加上此模板的编辑者需在[讨论页](https://zh.wikipedia.org/wiki/Talk:AJAX)说明此章节中立性有争议的原因，以便让各编辑者讨论和改善。 |
| ---------------------------------------- | ---------------------------------------- |
|                                          |                                          |

对程序员而言，开发Ajax应用最头痛的问题莫过于以下几点：

- Ajax在本质上是一个浏览器端的技术，首先面临无可避免的第一个问题即是浏览器的兼容性问题。各家浏览器对于[JavaScript](https://zh.wikipedia.org/wiki/JavaScript)／[DOM](https://zh.wikipedia.org/wiki/DOM)／[CSS](https://zh.wikipedia.org/wiki/CSS)的支持总有部分不太相同或是有Bug，甚至同一浏览器的各个版本间对于[JavaScript](https://zh.wikipedia.org/wiki/JavaScript)／[DOM](https://zh.wikipedia.org/wiki/DOM)／[CSS](https://zh.wikipedia.org/wiki/CSS)的支持也有可能部分不一样。这导致程序员在写Ajax应用时花大部分的时间在[调试](https://zh.wikipedia.org/wiki/%E8%B0%83%E8%AF%95)浏览器的兼容性而非在应用程序本身。因此，目前大部分的Ajax链接库或开发框架大多以js链接库的形式存在，以定义更高阶的JavaScript API、JavaScript对象（模板）、或者JavaScript Widgets来解决此问题。如prototype.js。
- Ajax技术之主要目的在于局部交换客户端及服务器之间的数据。如同传统之主从架构，无可避免的会有部分的业务逻辑会实现在客户端，或部分在客户端部分在服务器。由于业务逻辑可能分散在客户端及服务器，且以不同之程序语言实现，这导致Ajax应用程序极难维护。如有用户接口或业务逻辑之更动需求，再加上前一个JavaScript/DOM/CSS之兼容性问题，Ajax应用往往变成程序员的梦魇。针对业务逻辑分散的问题，Ajax开发框架大致可分为两类：


- 将业务逻辑及表现层放在浏览器，数据层放在服务器：因为所有的程序以JavaScript执行在客户端，只有需要数据时才向服务器要求服务，此法又称为胖客户端（fat client）架构。服务器在此架构下通常仅用于提供及储存数据。此法的好处在于程序员可以充分利用JavaScript搭配业务逻辑来做出特殊的用户接口，以匹配终端用户的要求。但是问题也不少，主因在第一，JavaScript语言本身之能力可能不足以处理复杂的业务逻辑。第二，JavaScript的执行性能一向不好。第三，JavaScript访问服务器数据，仍需适当的服务器端程序之配合。第四，浏览器兼容性的问题又出现。有些Ajax开发框架如DWR企图以自动生成JavaScript之方式来避免兼容的问题，并开立通道使得JavaScript可以直接调用服务器端的Java程序来简化数据的访问。但是前述第一及第二两个问题仍然存在，程序员必须费相当的力气才能达到应用程序之规格要求，或可能根本无法达到要求。


- 将表现层、业务逻辑、及数据层放在服务器，浏览器仅有用户接口引擎（User Interface engine）；此法又称为瘦客户端（thin client）架构，或中心服务器（server-centric）架构。浏览器的用户接口引擎仅用于反映服务器的表现层以及传达用户的输入回到服务器的表现层。由浏览器所触发之事件亦送回服务器处理，根据业务逻辑来更新表现层，然后反映回浏览器。因为所有应用程序完全在服务器执行，数据及表现层皆可直接访问，程序员只需使用服务器端相对较成熟之程序语言（如Java语言）即可，不需再学习JavaScript/DOM/CSS，在开发应用程序时相对容易。缺点在于用户接口引擎以及表现层通常以标准组件的形式存在，如需要特殊组件（用户接口）时，往往须待原框架之开发者提供，缓不济急。如开源码Ajax开发框架[ZK](https://zh.wikipedia.org/wiki/ZK)目前支持XUL及XHTML组件，尚无XAML之支持。

Ajax是以异步的方式向服务器提交需求。对服务器而言，其与传统的提交窗体需求并无不同，而且由于是以异步之方式提交，如果同时有多个Ajax需求及窗体提交需求，将无法保证哪一个需求先获得服务器的响应。这会造成应用程序典型的多进程（process）或多线程（thread）的竞争（racing）问题。程序员因此必须自行处理或在JavaScript里面动手脚以避免这类竞争问题的发生（如Ajax需求未响应之前，先disable提交按钮），这又不必要的增加了程序员的负担。目前已知有自动处理此问题之开发框架似乎只有[ZK](https://zh.wikipedia.org/wiki/ZK)。[[来源请求\]](https://zh.wikipedia.org/wiki/Wikipedia:%E5%88%97%E6%98%8E%E6%9D%A5%E6%BA%90)
## javaScript的实现
一个完整的javaScript实现应该由下列三个不同的部分组成  
1.核心（ECMAScript）  
2.文档对象模型（DOM）  
3.浏览器对象模型（BOM）

---

### ECMAScript
ECMA规定了JS的组成部分：语法    类型    语句    关键字  保留字  操作符  对象

---

### 文档对象模型（DOM | Document Object Model）
文档对象模型是针对XML但经过扩展用于HTML的应用程序编程接口（API）。DOM把整个页面映射为一个多层点结构。
```
<html>
    <head>
        <title></title>
    </head>
    <body></body>
</html>
```
通过DOM创建的这个表示文档的树形结构，开发人员活动控制页面的结构的主动权。借助DOM提供的API，开发人员可以轻松的操作任何节点  

#### DOM2

如果说DOM1的主要目标是映射文档结构。那么DOM2的目标就大很多了
DOM2引入新模块：  
1.DOM Views：为文档定义了基于样式信息的不同视图。   
2.DOM  Events:说明了如何使用事件与DOM进行交互。  
3.DOM  Style:定义了如何以编程的方式来访问和改变CSS样式的信息。  
4.DOM  Traversal and Range:引入了遍历DOM和选择其特定部分的新接口。  

#### DOM3
DOM3 引入了统一方式加载和保存文档---在DOM加载和保存模块中定义。
新增了DOM验证，验证文档的方法。

---

### 浏览器对象模型（BOM | Browser Object Model）
从根本上讲 BOM只处理浏览器窗口和框架，但是人们习惯把所有的针对浏览器的JavaScript扩展算作BOM的一部分。

# 操作dom

## 一、获取dom
依据id获取元素
```js
var el = document.getElmentById('id');
```
依据class获取元素
```js
var els = document.getElementsByClassName('class');
```
依据标签名获取元素
```js
var els = document.getElementsByTagName('tag');
```
依据选择器获取元素
```js
var el = document.querySelector('selector');
var els = document.querySelectorAll('selector');
```

## 二、操作元素属性
获取元素属性
```js
var attr = el.<attrName>
```
修改元素属性
```js
attr.<attrName> = <value>
```
实例：
```js
var id = el.id; // 获取元素id属性
el.id = 'newId'; // 设置元素id属性
```

## 三、操作元素class
* ### className方式
获取class
```js
var className = el.className;
```
添加class
```js
el.className += ' <newClass>';
```
删除等操作也是对className字符串的操作，这里省略。
* ### classList方式
获取class数组
```js
var classList = el.classList;
```
添加class
```js
el.classList.add('<newClass>');
```
删除class
```js
el.classList.remove('<class>');
```
是否包含某个class
```js
el.classList.contains('<class>');
```
切换class
```js
el.classList.toggle('<class>');
```
按索引访问class
```
el.classList.item('<idx>');
```
## 四、操作dataset
html5新增了data-*的自定义属性方式。
定义方式
```html
<div id="demo" data-myData="myData"></div>
```
获取dataset定义的数据
```js
var el = document.getElmentById('demo');
var myData = el.dataset.myData;
```
## 五、操作style
js访问css属性时，使用驼峰命名方式访问<br />
获取style
```js
var backgroundColor = el.style.backgroundColor;
```
设置style
```js
el.style.backgroundColor = '#000';
```
## 六、创建、插入、替换、复制和移除dom
创建dom
```js
var el = document.createElment('<tag>');
```
插入dom
```js
parent.appendChild(el); // 将dom插入到容器的最后面
parent.insertBefore(newEl, exsitedEl); // 将dom插入到容器某个子元素的前面
```
替换dom
```js
parent.replaceChild(newEl, oldEl);
```
复制dom
```js
el.cloneNode(false); // 浅拷贝，只复制当前结点
el.cloneNode(true); // 深拷贝，复制当前结点及其子孙结点
```
移除dom
```js
parent.removeChild(el); // 移除容器的el子元素
```
# 七、操作dom结点属性
获取结点内容
```js
var text = el.innerText; // 获取结点的文本内容
var html = el.innerHTML; // 获取结点中的dom内容
```
获取结点名称
```js
var nodeName = el.nodeName;
```
获取结点值
```js
var nodeValue = el.nodeValue;
```
获取结点类型
```js
var nodeType = el.nodeType;
```
获取父节点
```js
var parentNode = el.parentNode;
```
获取子结点
```js
var childNodes = el.childNodes;
```
> 笔记：
> nodeType、nodeName可以用于判断标签类型

## 八、文档信息
document对象可以操控部分文档相关信息。
```js
var title = document.title; // 文档标题
var url = document.URL; // 文档url
var domain = document.domain; // 文档域名
var referrer = document.referrer; // 返回载入当前文档的来源文档的URL
```
> 笔记：
> domain可以被设置，可以用于解决内嵌框架跨域问题。
> 比如，一个页面的domain为www.wrox.com，而内嵌页面为www.p2p.wrox.com
这样把两个页面的domain都设置为wrox.com可以解决跨域。
```js
document.domain = 'wrox.com';
```
> 值得注意的是：松散的domain不能设置成紧绷的domain
```js
document.domain = 'wrox.com'; // 松散的
document.domain = 'p2p.wrox.com'; // 紧绷的
```

## 九、特殊集合
document对象具有一些特殊的集合，支持快速访问页面某些元素
```js
document.anchors // 返回所有带name的a标签
document.links // 返回所有带href的a标签
document.forms // 返回所有的form标签
document.images // 返回所有的img标签 
```

## 十、操作特性
除了直接使用点运算符访问结点特性外，还可以使用getAttribute等属性操作特性。
```js
el.getAttribute('<attr>'); // 获取特性值
el.setAttribute('<attr>', <value>); // 设置特性
el.removeAttribute('<attr>'); // 移除特性 
```
除了上面常见的用法外，元素还存在attributes属性，它是元素结点中的所有属性结点的集合。
```js
el.attributes.getNamedItem('<attr>').nodeValue; // 获取属性结点的结点值
el.attributes.removeNamedItem('<attr>'); // 移除属性结点
// 添加属性结点
var attrNode = document.createAttribute('<attr>'); // 创建属性结点
attrNode.nodeValue=<value>; // 设置属性结点的结点值 
el.attributes.setNamedItem(attrNode); // 设置元素的属性结点
```
> 笔记：
> 1. 除了使用getNamedItem等方法外，attributes属性也可以使用`[]`操作符访问和赋值。
> 2. 一般而言，attributes属性并不常用，除非要遍历一个元素结点中所有的特性时才会用到。
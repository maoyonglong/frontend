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

## 八、操作文档信息
document


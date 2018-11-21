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
* className方式
获取class
```js
var className = el.className;
```
添加class
```js
el.className += ' <newClass>';
```
删除等操作也是对className字符串的操作，这里省略。
* classList方式
获取class数组
```js
var classList = el.classList;
```
添加class
```js
el.classList.add(<newClass>);
```
删除class
```js
el.classList.remove(<class>);
```
是否包含某个class
```js
el.classList.contains(<class>);
```
切换class
```js
el.classList.toggle(<class>);
```
class的索引
```
el.classList.item(<class>);
```
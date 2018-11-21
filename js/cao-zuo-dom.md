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
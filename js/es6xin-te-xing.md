# ES6新特性
## 一、let和const
我们知道，var定义的变量是不具备块级作用的。为了解决这个问题，es6引入了let关键字；而为了定义常量，引入了const关键字。
* ###let
* let声明的函数具有块级作用域。
```js
for(let i = 0; i < 10; i++){
    els[i].addEventListener(function(){
        console.log(i);
    }, false);
}
```
上面代码中用let定义i，会在每次循环中创建一个独立的块级作用域，这样保证了i的独立，上面的代码就是正确的。而如果使用var定义i，那么代码会出错，点击所有的el都会在控制台打印10.
* let声明的变量在同一个作用域不能重复定义，并且需要先定义才能使用
```js
let a = 2;
let a = 3; // 报错，不能重复声明
b = 1; // 报错，因为let定义变量不会变量提升，所以此时b未定义
let b; 
```
* ###const
* const声明的非引用类型常量不能修改
```js
const PI = 3.1415926;
PI = 3.14; // 报错，不能改变常量
```
* const声明的引用类型常量内容可变，指向不可变
```js
const arr = ['a', 'b'];
arr.push('c'); // arr->['a', 'b', 'c'] // 可以改变内容
arr = ['d']; // 报错，不能改变指向
```
## 二、模板字符串
以前，如果要创建多行字符串或者字符串中插入变量，需要使用反斜杠和`+`运算符，这让字符串显得十分复杂。es6引入了模板字符串，它使用反引号声明。
* 简单例子
```js
let msg = 'message'; 
let str = `
    <p>${msg}</p>
`;
```
> 笔记：
> 模板字符串使用`${}`插入变量，为了方便记忆，我简单把它叫做插值。
* 表达式插值例子 <br />
插值不仅仅支持变量，可以是一般的js表达式。
```js
let count = 10;
let price = 0.25;
let message = `${count} items cost $${(count * price).toFixed(2)}.`;
console.log(message); // "10 items cost $2.50."
```
> 笔记：
> 1. 插值可以是js表达式。
> 2. 当模板字符串中连续出现两个`$`符号，第一个符号表现为美元符号，不是插值。
* 插值嵌套例子
```js
const arr = ['item1', 'item2'];
let str = `
    The elements of arr are: 
    ${
      arr.map(function(item, idx){
          return `${idx+1}、${item}`;
      }).join('\n')
    }
`
console.log(str);
/**
"
The elements of arr are:
1、item1
2、item2"
*/
```
* 标签模板 <br />
标签其实是函数，而标签模板就是把模板字符串作为实参的一种特殊的函数调用。
```js
// tag函数
const transferHtml = function(iterals, ...substitution){
    let dict = {
        "&" : "&amp;",
        "<" : "&lt;",
        ">" : "&gt;"
    };
    let result = "";
    let keys = Object.keys(dict);
    let re = new RegExp("["+keys.join("")+"]", "g");
    for(let i = 0; i < substitution.length; i++){
        let item = substitution[i];
        result += iterals[i];
        result += item.replace(re, function(match){
            return dict[match];
        });
    }
    result += iterals[iterals.length-1];
    return result;
};
transferHtml`${'<p>pppp</p>'}`; // 调用标签模板
// 结果："&lt;p&gt;pppp&lt;/p&gt;"
```
> 笔记：
> 1. tag函数的iterals保存着模板标签被插值分割的字符串`（参考split）`，如果插值在字符串最后，那么iterals的最后一个值的空字符串`""`；而substitution是插值的集合，它不是数组类型，而是类数组类型`（参考substitution）`
> 2. 如果需要把for循环代码改为substitution.forEach，那么substitution一定要使用`...`运算符展开这个类数组对象。

## 三、箭头函数
es6简化了函数的语法表示，一定程度上改善了函数调用时this指针指向多变的问题。
* 声明方法
```js
const add = (arg1, arg2) => {
    return arg1 + arg2;
};
/**等价于
function add(arg1, arg2){
    return arg1 + arg2;
}
*/
// 如果函数体简单，并且存在返回值可以再简写：
// const add = (arg1, arg2) => arg1+arg2;
```
* this指向 <br />
箭头函数的this指向声明它时所在的对象作用域（全局作用域是global对象的作用域）。
```js
const func = () => { console.log(this); };
const obj = {};
func.call(obj); // window（浏览器环境下）
```
> 笔记：
> 1. 箭头函数的this和调用对象无关（call、apply失效），只有声明时所在作用域有关。
> 2. 箭头函数没有arguments对象，可以用rest参数代替
> 3. 箭头函数不能作为构造函数
> 4. 箭头函数不能使用yield

## 四、函数参数默认值和rest参数
es6允许函数使用参数默认值，rest参数用于将参数转成数组。
```js
// 默认值
const func1 = (arg="arg") => {
    console.log(arg);
};
func1(); // "arg"
func1("arg1"); // "arg1"
// rest参数
const func2 = (...args) => {
    console.log(args);
};
func2(1,2,3); // [1, 2, 3];
```
> 笔记：
> rest参数使用`...`操作符指定，它是一个由实参组成的数组

## 五、解构赋值
es6可以依据结构进行赋值，简化了赋值操作。
* 解析结构对相应变量进行赋值
```js
let {a, b: c, d: d=1} = {a: 'a', 'b': 'b'};
console.log(a + '---' + c + '---' + d); // a---b---1
let [f, g, h=2] = [1, 2];
console.log(f + '---' + g + '---' + h); // 1---2---2
```
> 笔记：
> 1. `{a} = {a: 'a'};`实际上是`{a: a} = {a: 'a'}`通过a作为key值查找到对应的value进行赋值。
> 2. 数组的解构赋值将对应idx的值进行一一对应，进行相关赋值。
> 3. 对于默认值，如果对应位置等号右边的值为undefined，那么等号左边对应的变量使用默认值。
```js
let [a, b=2, c] = [1, undefined, 3];
console.log(a + '---' + b + '---' + c); // 1---2---3
```


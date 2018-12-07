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
* 声明变量时使用解构赋值
```js
let a = 1;
let b = 2;
let obj = {a, b};
console.log(obj); // {a: 1, b: 2}
```
* 在函数参数中使用解构赋值
```js
function func({a, b} = {'a', 'b'}){
    console.log(a, b);
}
func({a: 1}); // 1 'b'
```
## 六、Promise
Promise对象可以将异步编程（特别是ajax）变成链式调用形式，更具可读性和可维护性。
* 简单getJSON函数的封装
```js
const getJSON = (url) => {
    return new Promise(function(resolve, reject){ // 执行函数
        const xmlHttp = window.XMLHttpRequest ? new XMLHttpRequest() : new ActiveXObject("Microsoft.XMLHTTP");
        xmlHttp.open('GET', url, true);
        xmlHttp.send();
	    xmlHttp.onreadystatechange=function(){
		    if (xmlHttp.readyState==4 && xmlHttp.status==200){
		        try{
		            let response = JSON.parse(xmlHttp.responseText);
			        resolve(xmlHttp.response); // 
		        }catch(e){
		            reject(e);
		        }
		    }else{
		        reject(new Error(xmlHttp.statusText)));
		    }
	    }
    }).
    // 执行函数代码正常时进行后续处理
    then(function(res){
        console.log(res);
    }).
    // 执行函数代码错误时进行的后续错误处理
    catch(function(e){
        console.log(e);
    });
}
```
> 笔记：
> 1. promise对象在创建时立即执行执行函数，立即执行函数用于分配任务，在执行函数中调用resolve（）和reject()函数，将分别触发then和catch函数任务。
> 2. then和catch执行完成会返回一个新的Promise对象实例，故可以链式调用。
> 3. 如果执行函数或者then方法抛出异常，catch方法可以捕获异常并且执行
* 已决或已拒绝Promise对象
```js
// 已决Promise
let promise1 = Promise.resolve(<param>);
// 已拒绝Promise
let promise2 = Promise.reject(<param>);
// 已决定了执行后状态的Promise可以直接调用then或者catch
promise1.then(function(param){
    console.log(param);
});
promise2.catch(function(param){
    console.log(param);
});
```
* 非Promise的Thenable对象
```js
/** 
当一个非Promise对象拥有一个能接受 resolve 与 reject 参数的 then() 方法，这个对象被称为非Promise的Thenable对象；
它能被Promise.resolve和Promise.reject方法调用。
*/
let thenable1 = {
    then: function(resolve, reject) {
        resolve('resolve');
    }
};
let thenable2 = {
    then: function(resolve, reject) {
        reject('reject');
    }
};
let t1 = Promise.resolve(thenable1); // 'resolve'
t1.then(function(value){
    console.log(value);
});
let t2 = Promise.resolve(thenable2); // 'reject'
t2.catch(function(value){
    console.log(value);
});
```
* 串行Promise
```js
/**
    then方法可以连续多个，使用return返回值进行参数传递
*/
let p1 = new Promise(function(resolve, reject) {
    resolve(42);
});
p1.then(function(value) {
    console.log(value); // 42
    return value + 1; // 传递到下一个then的参数
}).then(function(value) {
    console.log(value); // 43
});
```
* ###多Promise对象处理
* Promise.all() <br />
使用Promise处理异步操作时，当一个异步操作需要在多个异步操作执行完成后执行，那么可以使用Promise对象all表示这种逻辑。
```js
let p1 = new Promise(function(resolve, reject) {
    resolve(42);
});
let p2 = new Promise(function(resolve, reject) {
    resolve(43);
});
let p3 = new Promise(function(resolve, reject) {
    resolve(44);
});
let p4 = Promise.all([p1, p2, p3]);
// p4在p1、p2、p3都执行完才执行
p4.then(function(value) {
    console.log(Array.isArray(value)); // true
    console.log(value[0]); // 42
    console.log(value[1]); // 43
    console.log(value[2]); // 44
});
```
* Promise.race <br />
类似all方法，如果需要表示一个Promise在多个Promise对象中存在一个执行完成才执行的逻辑，可以使用Promise对象的race方法。
```js
let p1 = new Promise(function(resolve, reject) {
    resolve(42);
});
let p2 = new Promise(function(resolve, reject) {
    resolve(43);
});
let p3 = new Promise(function(resolve, reject) {
    resolve(44);
});
let p4 = Promise.race([p1, p2, p3]);
// p4在p1、p2、p3中的一个执行完才执行
p4.then(function(value) {
    console.log(value); // 42
});
```
> 笔记：
> all和race创建的Promis都会在一个Promise返回拒绝状态时，立即执行，并呈现拒绝状态，执行catch方法，而不需要等待其它Promise的执行。

## 七、set和map
es6新增了set和map集合，set是一种成员唯一的类似数组的集合，map是一种类似js字面量对象（JSON）的键值对集合（键不仅可以是字符串还可以是对象）。
* set
```js
// 普通set
// ---------------------------
let set1 = new Set();
set1.add(5); // 添加2
set1.add(5); // 重复会被忽略
let set2 = new Set([1, 2]); // 使用数组创建Set
set2.has(2); // 判断set2是否存在2
set2.delete(2); // 删除2
set2.clear(); // 清空set2
set2.size; // set2的长度
set2.forEach(function(){}, this); // set可以使用forEach
let arr = [...set1]; // set转成数组
// Weak Set
// Weak Set只能存储引用类型，能够保证set的对象元素被设为null时，会被垃圾回收机制回收。
// ------------------------------
let weakSet1 = new WeakSet(); 
let weakSet2 = new WeakSet([1, 2]);
// weak set的操作与set一致。
```
* map
```js
// 普通map
// -------------------------
let map = new Map(); // 初始化空的map
map.set('key', 'value'); // 添加键值对
map.get('key'); // 获取键值对
map.has('key'); // 判断是否存在键值对
map.delete('key'); // 删除键值对
map.clear(); // 清空map
map.size; // 键值对的个数
map = new Map([['key1', 'key2'], ['val1', 'val2']]); // 使用数组创建map
map.forEach(function(){}, this); // map可以使用forEach
// Weak Map
// Weak Map只能存储键是引用类型的键值对，作用与weak set一样。
// -----------------------------
let weakMap = new WeakMap();
let key = {};
weakMap.set(key, 'val');
```
> 笔记：
> 1. set和map都具有has、delete、clear和forEach方法，也都存在着各自的迭代方式（见迭代器）。
> 2. weakset和weakmap都不能对内容进行过度操控，没有forEach、delete、clear方法，没有迭代器方式，没有size属性。

## 八、迭代器和生成器
es6新增了迭代器用于处理循环遍历问题，而生成器则是用于生成迭代器的函数。
* 迭代器与迭代对象
```js
// 迭代器是使用next方法一步一步遍历元素的对象
// es5实现迭代器
function createIterator(items){
    var i = 0;
    return {
        next: function(){
            var done = i >= items.length; // 遍历是否完成
            var value = !done ? value[i++] : undefined; 
            return {
                done: done,
                value: value
            };
        }
    };
}
var iter = createIterator([1,2,3]); // 创建遍历数组的迭代器
iter.next(); // 返回下一个元素 
// es6迭代对象
let arr = [1,2,3]; 
// 数组是可迭代对象，因为具有Symbol.iterator属性
// 该属性是一个函数，它用于创建默认迭代器arr[Symbol.iterator]();
// js引擎后台在of关键字使用时，自动调用该函数创建迭代器，并使用next等方法自动遍历可迭代对象
for(let item of arr){
    console.log(item);
}
```
* 生成器
```js
// 带星号的函数被称为generator（生成器）
// 普通生成器
function *generator(){
    yield 1;
    yield 2;
    yield 3;
}
let iter = generator(); 
// 生成器会依据yield返回迭代器对象，每个yield的返回都会暂停执行函数，等待迭代器对象使用下一个值才执行。
iter.next().value; // 1
iter.next().value; // 2
iter.next().value; // 3
// 传参生成器
function *createIterator(){
    // 先执行yield返回后，再执行赋值操作
    let first = yield 1;
    let second = yield frist + 2;
    let third;
    try{
        third = yield second + 3;
    }catch(e){
        third = 'throw error';
    }
    return; // 提前结束generator
    yield 2;
} 
let iter = createIterator();
iter.next(2).value; // 1
iter.next(3).value; // first+2 -> 3
iter.next(new Error('error')); // throw error
iter.next().value; // undefined 
// 生成器委托 
// 生成器委托其实像函数把相同的代码进行封装，函数里面调用多个函数的情况
function subIterator1(){
    yield 1;
    yield 2;
}
function subIterator2(){
    yield 3;
    yield 4;
}
function *createIterator(){
    yield *subIterator1();
    yield *subIterator2();
}
let iter = createIterator();
let item;
do{
    item = iter.next();
    console.log(item.value);
}while(!item.done);
// 结果：
// 1
// 2
// 3
// 4
// undefined
```
* 任务执行器
```js
function run(taskDef){
    let task = taskDef(); // 创建迭代器
    let result = task.next(); // 启动任务，步骤执行1次
    // 循环步骤
    function step(){
        // 如果任务未完成{
        if(!result.done){
            // 是否是执行任务的逻辑函数
            if(typeof result.value==='function'){
                result.value(function(err, data){
                    if (err) {
                        result = task.throw(err);
                        return;
                    }
                    result = task.next(data);
                    step();
                });
            }else{
                result = task.next(result.value);
                step();
            }
        }
    }
    // 执行循环函数
    step();
}
// 使用
let fs = require("fs");
function readFile(filename) {
    return function(callback) {
        fs.readFile(filename, callback);
    };
}
run(function*() {
    let contents = yield readFile("config.json");
    doSomethingWith(contents);
    console.log("Done");
});
```
> 笔记：
> 1. 字符串、数组、map、set、object、NodeList都可以使用of进行遍历，它们是可迭代对象。
> 2. values()、keys()、entries()方法都会返回一个可迭代对象

## 九、对象和类
es6的类使用class关键字来声明，它增强了原型继承方式，可以使用extend关键字来声明继承关系，还增加了新的方法定义方式、super关键字等内容。
* 对象方法简写 
```js
let obj = {
    name: 'obj',
    getName() {
        // 简写方式允许使用super();
        return this.name;
    }
};
```
* 对象变量名属性
```js
let lastName = 'lastName';
let obj = {
    'firstName': 'first',
//    [lastName]: 'second'
};
// 或者
let suffix = 'Name';
let obj = {
//    ['first' + suffix]: 'first',
//    ['second' + suffix]: 'second'
};
```
* 对象相关原型方法
```js
Object.create(Array); // 返回原型为Array的对象，并且可以使用prototype访问；并非只有\_\_proto\_\_属性
Object.getPrototypeOf(obj); // 获取obj的原型对象
Object.setPrototype(obj， Object); // 设置obj的原型对象为Object
```
* super
```js
// 不使用super访问原型方法
let person = {
    name: 'Person',
    getName() {
        return this.name;
    }
};
let son = {
    name: 'Son',
    getName() {
        // 访问原型中的方法
        return Object.getPrototypeOf(this).getName.call(this);
    }
};
Object.setPrototypeOf(son, person);
son.getName(); // son
/*
    然而，如果原型链过长，并不好用；
    下面代码出现栈溢出错误。这是因为:
    mike调用getName时this是mike，
    而它的原型是son,
    故反复调用son的getName方法   
*/
let mike = Object.create(Object);
Object.setPrototypeOf(mike, son);
mike.name = 'mike';
mike.getName();
```
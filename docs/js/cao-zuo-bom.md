# 操作BOM

## 一、前言
BOM是指浏览器对象模型，涉及和浏览器相关信息的对象，有window对象及其属性location、navigator、screen和history对象。

## 二、window对象
window对象表示浏览器的一个实例。在浏览器中，它既是js访问浏览器窗口的一个接口，也是ECMAScript标准中的global对象。
* ### 全局作用域
由于window对象又是global对象，所以，全局定义的变量、函数都会变成window对象的属性和方法。
```js
var a = 1;
var func = function(){
    console.log('func');
};
console.log(window.a); // 1
console.log(window.func); // ƒ (){ console.log('func'); }
```
> 笔记：
> window是浏览器环境中的global对象。
> 直接定义的window属性方法可删除，而依靠global对象特性挂载都window中的属性和方法不可删除。
```
var a = 1;
window.b = 2;
delete window.a; // false，ie8及以下报错
delete window.b; // true
```
* ### 框架
页面中的每个框架都有自己的window对象，它们保存在frames集合中，可以通过idx或者框架的name属性的值来访问对应的window对象。
```js
var frame0 = window.frames[0]; 
var frameMyName = window.frames['myName'];
```
> 笔记：
> 1. 这里最好把window对象改为top，使用top.frames来获取对应的window；这是因为top对象是指最外层框架对象，也就是浏览器窗口对象，或者说把内嵌框架视为内嵌页面的话，top就是主页面对象。
> 2. 可以使用window.parent获取当前框架的父框架对象
* ### 导航和打开窗口
使用window.open()方法可以打开一个新的窗口，它的参数如下：
| 参数 | 说明 |
| --- | --- |
| url | 新窗口的url |
| target | 指定载入html文档的框架（可以是iframe，也可以是新的浏览器窗口）|
| specs | 特殊描述，指定新窗口一些信息，如大小 |
| replace | true-->替换浏览历史当前条目; false-->新增浏览历史条目 |
在已有框架载入新页面
```js
window.open('https://baidu.com', 'myFrame'); // 在name等于myFrame的框架中载入baidu搜索页面
```
> 笔记：
> 1. 如果给定的target值的框架不存在，那么会新开一个窗口，命名为该值。
> 2. 打开默认新标签页，可以将target设置为_blank

弹出窗口，也可以在后续改变设置
```js
var myFrameWin = window.open('https://baidu.com');
myFrameWin.resizeTo(<x>, <y>);
myFrameWin.moveTo(<x>, <y>);
myFrameWin.close();
myFrameWin.closed; // 是否已关闭
myFrameWin.opener; // 打开该弹窗的窗口（window）对象
```
窗口屏蔽检测脚本
```js
var blocked = false;
try{
    var popup = window.open('https://baidu.com');
    if(popup === null){
        blocked = true;
    }catch(e){
        blocked = true;
    }
    if(blocked){
        console.log('The popup was blocked');
    }
}
```
* ### 对话框
浏览器内置的对话框主要有alert、confirm和prompt三种。而find和print对话框并不常用，这里介绍。
alert警告框
```js
alert(<msg>);
```
确定框
```js
var flag = confirm('<ques>');
if(flag){
    console.log('单击Ok会返回true');
}else{
    console.log('关闭窗口会返回false');
}
```
提示输入框
```js
var ans = prompt('<ques>', '<tipAns>');
if(ans !== null){
    console.log('输入的文本是：' + ans);
}else{
    console.log('关闭窗口返回null');
}
```
## 三、location对象
location对象保存地址和导航等相关属性和方法，它是window对象的一个属性。
以https://www.bilibili.com/video/av32433036为例
```js
location.href // 完整url,"https://www.bilibili.com/video/av32433036"
location.protocol // 协议，"https:"
location.host // 域名加端口号，"www.bilibili.com"
location.hostname // 域名，"www.bilibili.com"
location.port // 端口号，""
location.pathname // 目录，"/video/av32433036"
location.hash // 哈希#，""
location.search // 查询字符串，""
```
> 笔记：
> 1. 如果是默认端口80，那么port为""。
> 2. 查询字符串是指?q=123等以问号开头的部分。

* ######获取查询字段脚本
```js
function getQueryArgs(){
    var qs = location.search;
    qs = qs.length > 0 ? qs.substring(1) : ''; // 查询字符串
    var args = {}; // 保存字段的对象
    var items = args.split('&'); // 获得每一项key=value
    for(var i = 0, len = items.length; i < len; i++){
        var tmp = items[i].split('=');
        var key = decodeURLComponent(tmp[0]); 
        var value = decodeURLComponent(tmp[1]); 
        // 如果key存在
        if(key.length > 0){
            args[key] = value;
        }
    }
    return args;
}
```
> 笔记：
> 获取查询字符串的内容需要使用decodeURLComponent方法进行解码。
* ######浏览器位置操作
页面跳转可以通过location.assign()和location.replace()方法或者设置相关属性实现。
```js
// 方法
location.assign('<url>'); // 载入新文档
location.replace('<url>'); // 载入新文档
location.reload(); // 重载当前文档（可能从浏览器缓存中加载）
location.reload(true); // 重载当前文档（从服务器中加载） 
// 属性
location.href = '<url>';
location.hash = '<newHash>';
... // 其它能改变url的属性
```
> 笔记：
>  assign、href造成的跳转和replace造成的跳转的不同之处是前者保留当前页面的历史记录；而后者不保留，更换成新的url作为历史记录条目。

## 四、navigator对象
navigator对象保存着浏览器相关类型信息。比如浏览器版本、userAgent。
* ######检测插件
```js
// 非IE
// 非IE浏览器具有navigator.plugins属性
function hasPlugin(name){
    name = name.toLowerCase();
    var plugins = navigator.plugins;
    for(var i = 0; i < plugins.length; i++){
        var curPlugin = plugins[i];
        var curPluginName = curPlugin.name.toLowerCase();
        if(curPluginName.indexOf(name) >= 0){
            return true;
        }
    }
    return false;
}
alert(hasPlugin('Flash'));
// IE
// IE不具备navigator.plugins属性，它的插件使用COM对象实现的，需要用插件的COM对象唯一标识符识别。
function hasIEPlugin(name){
    try{
        new ActiveObject(name); // 尝试创建一个插件实例
        return true;
    }catch(e){
        return false;
    }
}
alert(hasIEPlugin('ShockwaveFlash.ShockwaveFlash'));
```
> 笔记：
> 1. 可以发现IE和其它浏览器检测插件的形式相差甚远，所以一般检测特定插件而不是通用插件的脚本比较实用，比如：
> ```js
    function hasFlash(){
        var result = hasPlugin('Flash');
        if(!result){
            result = hasIEPlugin('ShockwaveFlash.ShockwaveFlash');
        }
        return result;
    }
```

* ######注册处理程序
navigator对象新增的registerContentHandler和registerPrototcolHandler方法一个站点处理特定类型（MIME）的信息。
```js
// 指明处理rss的程序所在url及其名字
navigator.registerContentHandler("application/rss+xml", '<url>', '<appName>');
// 指明处理mailto协议的程序所在url及其名字
navigator.registerPrototcolHandler("mailto", '<url>', '<appName>');
```
> 笔记：
> 上面是注册处理程序常用场景：rss和电子邮件协议。

## 五、screen对象
screen对象保存与浏览器屏幕相关的信息。一般只在改变弹窗大小时使用。
改变弹窗大小
```js
window.resizeTo(screen.availWidth, screen.availHeight);
```
> 笔记：
> 有时，需要获取整个屏幕的宽高，这时，需要使用screen.width和screen.height

## 六、history对象
history对象保存与浏览器历史记录相关的属性和方法。
```js
history.go(<idx>|<url>); // 前进（正）或后退（负）、
跳转到最近相应页面
history.back(); // 后退
history.forward(); // 前进
history.length; // 历史记录条数
```

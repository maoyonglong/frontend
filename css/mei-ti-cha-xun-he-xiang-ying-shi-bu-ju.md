# 媒体查询和响应式设计

## 一、媒体查询
* #####简要说明
媒体查询是指使用css3新增的@media指令来判断媒体类型和屏幕宽度等设备和浏览器信息，来选择性的应用样式或者样式表。
* #####使用方法
    * ######基本语法
    [css媒体查询](https://developer.mozilla.org/zh-CN/docs/Web/Guide/CSS/Media_queries)
    * ######切换样式表
    ```html
    <link rel="stylesheet" src="mobile.css" media="screen and (max-device-width=480px)" />
    <link rel="stylesheet" src="computer.css" media="screen and (max-device-width=1920px)" />
    ```
    * ######切换样式
    ```css
    @media (max-width: 700px){
        ...
    }
    ```
* #####补充
媒体查询不兼容低版本浏览器（IE9-），如果需要兼容这些浏览器，可以使用js解决。可以使用[css3-mediaqueries.js](http://code.google.com/p/css3-mediaqueries-js/)解决。

##二、响应式设计
* #####简要说明
响应式设计是指确保一个页面在不同终端，不同屏幕的设备上，得到满意舒适的视觉体验的页面设计。实现响应式设计的方法不单一，只要能达到设计目标即可。所以，响应式设计更多的是设计层面上的。响应式布局主要依靠流体布局、弹性布局、网格布局配合媒体查询实现。
* #####本质
目前而言，响应式布局主要是在主流终端屏幕下断点，使用媒体查询将断点分开的各个屏幕对应着各自的样式表来实现不同屏幕样式不同的效果。而这些样式表一般都是流体布局、弹性布局和网格布局，在其对应的断点范围有较好的弹性，不至于让样式由明显的跳变。当然，还可以针对非屏幕尺寸响应样式，比如横屏和竖屏，但是，目前主要就是针对屏幕宽度。
* #####响应式图片
响应式图片可以由js和流体图片实现

```css
/* 流体图片 */
.fuild-img{
    max-width: 100%;
}
```
```js
// 获取屏幕可视区域宽度
var clientWidth = document.documentElement.clientWidth;
// 根据宽度决定载入图片的尺寸
if(clientWidth > 768){
    // img是图片dom元素
    img.src = "large-img.jpg";
}else{
    img.src = "small-img.jpg";
}
```
> 笔记：
1. 有时为了兼容IE，由于低版本IE不支持max-width，只能使用`width: 100%`设置流体图片的宽度,这时，可以添加js来切换样式。

```js
//判断是否是IE浏览器
function IEVersion(){
    var userAgent = navigator.userAgent; //取得浏览器的userAgent字符串
    var isIE = userAgent.indexOf("compatible") > -1 && userAgent.indexOf("MSIE") > -1 && !isOpera; //判断是否IE浏览器
    var isEdge = userAgent.indexOf("Windows NT 6.1; Trident/7.0;") > -1 && !isIE; //判断是否IE的Edge浏览器
    if(isIE){
        var reIE = new RegExp("MSIE (\\d+\\.\\d+);");
        reIE.test(userAgent);
        var fIEVersion = parseFloat(RegExp["$1"]);
        return fIEVersion;
    }else{
        return false;
    }
}
// 切换样式
if(IEVersion() < 8){
    img.style.width = "100%";
}
```
> 2.可以使用相应的js插件解决问题，比如[responsive-images.js](https://github.com/kvendrik/responsive-images.js)
> 3.除了使用百分比和max-width等属性以外，让元素依据内容自适应也是常用的方法，这时，可以加上margin，padding等微调布局。

* 响应式布局的步骤
    * ######在html文档的添加下面元信息标签
    ```html
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    ``` 
    * ######选择一个设计稿，完成布局
    一般选择最大或最小的设计稿作为最初的布局对象。如果只考虑移动端和PC端，这个选择就是移动端优先和PC端优先的选择。因为这是你希望完美实现最初的设计稿，而其它设计稿可能在其基础上需要添加微调，而且也不一定能完全还原设计稿效果。
    * ######在基本html上调整和修改样式
    将依据初稿完成的html在浏览器不同设备屏幕上调试，依据相应设计稿调整和修改样式。当然，这里每个设计稿对应这个媒体查询范围。


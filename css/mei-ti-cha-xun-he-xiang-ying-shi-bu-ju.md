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
        /判断是否是IE浏览器，包括Edge浏览器
     function IEVersion()
     {
        var userAgent = navigator.userAgent; //取得浏览器的userAgent字符串
        var isIE = userAgent.indexOf("compatible") > -1 && userAgent.indexOf("MSIE") > -1 && !isOpera; //判断是否IE浏览器
		var isEdge = userAgent.indexOf("Windows NT 6.1; Trident/7.0;") > -1 && !isIE; //判断是否IE的Edge浏览器
        if(isIE)
        {
             var reIE = new RegExp("MSIE (\\d+\\.\\d+);");
             reIE.test(userAgent);
             var fIEVersion = parseFloat(RegExp["$1"]);
             if(fIEVersion == 7)
             { return "IE7";}
             else if(fIEVersion == 8)
             { return "IE8";}
             else if(fIEVersion == 9)
             { return "IE9";}
             else if(fIEVersion == 10)
             { return "IE10";}
             else if(fIEVersion == 11)
             { return "IE11";}
             else
             { return "0"}//IE版本过低
        }
		else if(isEdge)
		{
			return "Edge";
		}
        else
        {
            return "-1";//非IE
        }
     }    
```
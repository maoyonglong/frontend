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

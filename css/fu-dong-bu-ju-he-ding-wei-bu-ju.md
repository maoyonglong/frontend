#浮动布局和定位布局

## 一、浮动布局
* #####简要说明

    浮动布局指的是使用浮动属性、浮动元素不重叠、宽度基于内容等特点以及清浮动手段，加上margin、padding等盒模型属性辅助元素定位的布局方式。
* #####浮动布局示意图
![浮动布局示意图](./imgs/float.jpg)
    
    其中：
    1.left表示左浮动，right表示右浮动。
    2.浮动元素不会覆盖浮动元素，所以漂浮元素按顺序排列。
    3.如果容器的宽度不足，元素会自动换行
    4.浮动元素不会撑开容器高度，需要清浮动才可以让容器高度自适应。
* #####相关知识
    * ######清浮动
    ```css
    /*方法一：clear清浮动*/
    .clearfix:after{
        content: '';
        display: block;
        clear: both; /*请除元素左右两边的浮动*/
    }
    /*方法二：overflow清浮动*/
    .overfw{
        overflow: hidden; /*形成BFC，计算浮动元素的高度*/
    }
    ```
    > 笔记：
    > 1.方法一的原理是在容器的子元素后面生成伪元素，然后让这个伪元素清除浮动
    > 2.方法二的原理是形成BFC，BFC会计算浮动元素的高度。其中，BFC是“块级格式化上下文”，把它理解成独立的一个块、一个空间（类似div）即可。但是，这个块比较特殊，它具有不会被浮动元素覆盖和计算容器中浮动元素高度的特点。
    > 3.形成BFC的方式是：脱离文档流，变成行内块级元素和溢出隐藏三种方式。
    * ######浮动元素与兄弟元素
    浮动元素是否遮盖非浮动兄弟元素其中一个依据是它们在在dom树（html文档）中的先后顺序。
    ```html
    <div class="left">left</div>
    <div class="normal">normal</div>
    <div class="right">right</div>
    ```
    ```css
    div{
        background-color: red;
        border: 1px solid black;
    }
    .left{
        float: left;
    }
    .right{
        float: right;
    }
    ```
    上面代码的结果是
    ![sibling-float-1](./imgs/sibling-float-1.jpg)
    <br />
    其中normal被left遮盖
    
    > 笔记：
    > 1.left先渲染，由于其浮动所以脱离文档流，然后到渲染normal，填充了left在文档流中空出来的位置，又由于它是块级元素，填满整行空间。最后，渲染right，由于整行空间被normal填满，所以right只能换行，然后右浮动。
    > 2.在html中和normal调换顺序，可以发现left和right都遮盖了normal，因为它们先渲染，脱离文档流，腾出了空间。
    
    另一个依据就是浮动元素不遮盖inline元素和BFC。
    ```html
    <div class="left">left</div>
    <div class="normal">normal</div>
    ```
    ```css
    div{
        background-color: red;
        border: 1px solid black;
    }
    .left{
        float: left;
    }
    .normal{
        overflow: hidden; /*形成BFC*/
    }
    ```
    结果为：
    ![sibling-float-2](./imgs/sibling-float-2.jpg)
    <br />
    其中left不遮盖normal，normal的宽度自适应为100%减去left的宽度。
    
    >笔记：
    >1.利用浮动元素不遮盖BFC的特点，可以使用BFC元素在浮动布局中的宽度自适应
    >2.除了BFC外，行元素一样不能被浮动元素遮盖。
    >3.要实现这样的自适应布局，渲染顺序也很重要，像这个例子，调换连个div的顺序，会导致left换行。
    
## 二、定位布局

* #####简要说明
    
    定位布局是一种相对于参照物进行定位的布局。

* #####定位布局示意图
    ![定位布局示意图](./imgs/position.jpg)
    其中：
    1.参照物的选取取决于定位元素的定位方式
    2.top、left、right和bottom都有正负值。在定位时，先将定位元素和参照物对应边重合`（使用left就左边框重合、right就右边框重合，top、left以此类推）`，像参照物框外移动的方向为负值，反之，为正值。
    
* #####相关知识
    * ######定位方式和相关特点
    | 定位方式 | 参照物 | 特点 |  
    | ---- | ---- | ---- |  
    | static | 无 | 默认定位方式，不参与定位布局 |  
    | relative | 自身 | 占有原来空间 |  
    | absolute | 最近非static定位的父元素 | 脱离文档流 |  
    | fixed | 浏览器可视窗口 | 脱离文档流 |  
    
    > 笔记：
    > 1. relative和absolute一般配合使用
    > 2. 在使用absolute和fixed布局时，由于定位元素脱离文档流，所以宽高不再受块级元素特性的影响，由内容和width等属性决定；由于脱离文档流造成的空间缺失，也没有办法使用类似清浮动的方式让容器高度自适应，只能使用height、margin等属性改善布局。
    
    * ######层级关系
    除了static定位以外的定位方式可以使用z-index来决定定位元素层级（叠加次序）
    * ######粘性布局
    除了上面的定位方式外，还有新增的sticky定位（粘性定位）方式。这种定位方式比较特殊，它会根据滚动条滚动位置来决定使用类static定位或者类fixed定位方式。当滚动条滚动，并没有隐藏该元素，它表现为类static定位，left等无效；当滚动条滚动到隐藏该元素的位置时，它表现为类fixed定位，left等属性此时生效。
    > 粘性布局兼容性不佳。
    
    
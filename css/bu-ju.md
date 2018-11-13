# 布局

## 一、网格布局（Grid Layout）
* __简要说明__  

    网格布局，其实就是用若干条横线和纵线交叉形成一个个格子，这些格子就是网格。通过这些网格位置控制布局，就是网格布局。所以说，网格布局就是先指定好一个个格子的位置和大小，然后，往格子里填内容，就达到了布局的目的。
    
* __网格布局示意图__
![网格示意图](./imgs/grid.jpg)
其中：
1.row和column表示行列轨道。
2.含有背景颜色的六个矩形块是六个网格，网格由行列轨道交叉形成。
3.相邻轨道之间的空白是间隔，有行列两种间隔。
4.有数字标号的表示网格线，在网格之间存在着分割线，这是网格线，它的宽为网格之间的间隔。
5.网格容器的直接子元素称为网格项目。
* __相关css属性__
    * ######声明布局
    ```css
    .grid-box{
        display: grid; /*网格布局容器*/
    }
    ```
    * ######声明网格模板
    行列轨道用于确定网格的模板。声明方式为：
    ```css
    .grid-box{
        grid-template-rows: 100px repeat(2, 1fr); /*行轨道*/
        grid-template-columns: repeat(2, 1fr 1fr); /*列轨道*/
        grid-column-gap: 10px; /*列间隔*/
        grid-row-gap: 4px;/*行间隔*/
    }
    ```
    > 笔记：
    > fr单位是等分剩余内容的单位，repeat()用于重复轨道宽度的声明，所以上面代码声明了一个三行四列的网格。
    * ######隐式网格
    像上面那样给出了完整的行列轨道，叫做显示网格。还有一种情况，就是只给出了行或者只给出了列，那么另外的轨道需要靠内容决定。
    ```css
    .grid-box{
        grid-template-column: 1fr 1fr;
        grid-auto-rows: minmax(200px, auto); /*隐式行轨道高度*/
    }
    ```
    ```css
    .grid-box{
        grid-template-rows: 1fr 1fr;
        grid-auto-columns: 200px; /*隐式列轨道宽度*/
    }
    ```
    > 笔记：
    > 1.只要网格数不够用，隐式网格就会增加一行或者一列。
    > 2.minmax(min, max)表示长度在[min, max]区间内。
    * ######项目定位
    在网格容器中定义主元素，是依据网格线而不是依据网格轨道实现的。网格容器中子元素还能使z-index生效，用于改变层级关系。
    ```css
    .grid{
        grid-column-start: 1; /*从列网格线1开始*/
        grid-column-end: 4; /*于列网格线4结束*/
        grid-row-start: 1; /*从行网格线1开始*/
        grid-row-end: 3; /*于列网格线3结束*/
        z-index: 2; /*层级为2*/
    }
    ```
    > 笔记：
    > 1.网格容器中只有直接子元素（网格项目）参与布局定位，其它元素符合文档流
    > 2.display:contents会使网格的直接子元素的盒子消失，那么它的子元素就变成了网格容器的直接子元素，会参与到网格布局中
    > 3.绝对定位的网格项目先相对于自身的grid-column/row-start定位，如果没有设置这些属性，那么特性和不同绝对定位元素一样相对于最近非static父元素定位。
    
# 二、弹性布局（Flexbox Layout）
* __简要说明__  

    弹性布局和网格布局非常相似，最大的区别是前者是一维的，只定义规则而不制定目标，而后者是二维的;制定模板。
    
* __弹性布局示意图__
![弹性布局示意图](./imgs/flex.png)
其中：
1.flex container是弹性盒子（弹性布局容器），而flex item是弹性布局项目。
2.弹性布局可以具有一条主轴(main axis)和多条交叉轴(cross axis)，多条交叉轴只有项目被迫换行时产生。轴用于定位，start为开始位置，end为结束位置
3.项目在主轴和交叉轴的方向上的大小为main size和cross size。
* 相关css属性
    * ######声明布局
    ```css
    .flex-box{
        display: flex;
    }
    ```
    * ######声明容器规则
    ```css
    .flex-box{
        flex-direction: row; /*主轴方向*/
        flex-wrap: wrap; /*是否换行*/
        justify-content: space-around; /*主轴对齐方式*/
        align-items: stretch; /*单交叉轴(单行)对齐方式*/
        align-content: flex-start; /*多交叉轴（多行）对齐方式*/
    }
    ```
    > 笔记：
    > 1.align-items和align-content分别只对单交叉轴和多交叉轴项目对齐起作用。
    > 2.flex-direction和flex-wrap可以简写成:
    ```csss
        flex-flow：<flex-direction> || <flex-wrap>
    ```
    * 项目尺寸
    ```css
    .flex{
        flex-grow: 1; /*剩余空间分配比例*/
        flex-shrink: 1;/*空间不足缩小比例*/
        flex-basis: auto;/*项目原尺寸*/
    }
    ```
    > 笔记：
    1.
    
    

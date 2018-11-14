# css基本样式
> 
复合属性按复合顺序排列
all-direction表示所有方位（顺序为top、right、bottom、left）
如非必要，忽略inherit、initial、unset

* 盒子样式

| 属性 | 复合属性 | 效果 |
| ---- | ---- | --- |
| width | | 元素内容宽度 |
| height | | 元素内容高度 |
| padding | all-direction| 对应方位元素内边距 |
| border| width | 元素边框 |
| | style | 线条样式 |
| | color | 边框颜色 |
| margin | all-direction | 元素外边距左 |
| overflow | x | 水平方向溢出处理 |
| | y | 垂直方向溢出处理 |
| box-sizing  |  | 限制盒子的大小 |
| box-shadow | h-shadow | 阴影水平偏移位置 |
| | v-shadow | 阴影垂直偏移位置 |
| | blur | 模糊半径 | 
| | spread | 阴影向外传播大小 |
| | color | 阴影颜色 |
| | inset | 阴影内置 |
> 笔记：
* 盒子属性中，border还有分开写的属性：

| border | 二级属性 | 复合属性1 | 复合属性2 | 效果 |
| ---- | ---- | ---- | ---- | ---- |
| | all-direction |all-direction-width | | 对应方位边框样式 |
| | radius | all-direction | | 边框圆角半径 |
| | image | source | | 图像url |
| | | slice | all-direction | 图像切片 |
| | | width | all-direction | 图像边界宽度 |
| | | offset | all-direction | 边框图像和边框的距离 |
| | | repeat | | 重复方式 |
> * box-sizing有两个属性值：border-box和content-box，分别表示border限定的盒子大小不变（自动改变元素内容盒子大小来适应）和表示元素内容盒子大小不变。
* 设置box-shadow，要明白默认阴影大小和元素大小一致；模糊半径和border-radius很像，把阴影圆角模糊；spread是在默认阴影下叠加阴影；inset是将阴影反转，改为内嵌。

* 文本样式

| 属性 | 复合属性 | 效果 |
| ---- | ---- | ---- |
| color | | 字体颜色 |
| line-height | | 行高 |
| font | style | 字体样式 |
| | variant | 字体异体 |
| | weight | 字体粗细 |
| | size/line-height | 字体大小/行高 |
| | family | 字体系列 |
| direction | | 文本书写方向 |
| letter-spacing | | 字符间距 |
| word-spacing | |单词间距 |
| white-space | | 空白处理 |
| text-overflow | | 溢出文本处理 |
| text-align | | 水平对齐方式 |
| text-justify | | 两端对齐处理方式 |
| text-indent | | 首行缩进 |
| text-transform | | 大小写和首字母大写 |
| text-shadow | h-shadow | 文本水平阴影偏移 |
| | v-shadow | 文本垂直阴影偏移 |
| | blur | 模糊半径 |
| | color | 阴影颜色 | 
| word-break | | 非CJK单词断行方式 |
| word-wrap | | 长单词（如url）换行方式 |
> 笔记：
* letter-spacing和word-spacing用于处理间距
* text-align有justify属性值，表示两端对齐，这时，可以用text-justify来设置两端对齐的处理方式
* text-shadow和box-shadow是相似的，区别仅仅在于text-shadow没有spread和inset属性值
* 一行显示不完文本，末尾添加省略号显示的方法：

```css
.ellipsis{
    white-space: nowrap; /*不换行*/
    overflow: hidden; /*溢出隐藏*/
    text-overflow: ellipsis; /*溢出文本显示省略号*/
}
```

* 表格样式

| 属性 | 复合属性 | 效果 |
| ---- | ---- | ---- |
| border-collapse | | 是否合并边框 |
| border-spacing | h | 相邻单元格之间的水平距离 |
| | v | 相邻单元格之间的垂直距离 |
| caption-side | | 表格标题位置 |
| empty-cells | | 空白单元格样式处理 |
| table-layout | | 列宽的决定方式 |
> 笔记：
* 表格标题可以放置在上下两个位置
* border-collapse的属性值是collapse和separate，分别表示合并和分离

* 表单样式

| 属性 | 复合属性 | 效果 |
| ---- | ---- | ---- |
| appearance | | 外观 |
| outline | color | 轮廓颜色 |
| | style | 轮廓类型 |
| | width | 轮廓宽度 |
> 笔记：
* appearance是用户外观样式，它可以选择让标签看起来像按钮、图标等，有兼容性问题，需要加前缀，而且一般用在移动端。
* outline一般指input输入框聚焦时显示的轮廓，设置和border类型，仅仅是复合顺序不同。

 * 列表样式
 
 
  | 属性 | 复合属性 | 效果 |
  | ---- | ---- | ---- |
  | list-style | type | 列表项标记方式 |
  | | position | 列表项位置 |
  | | image | 自定义列表图标标记 |
  > 笔记：
  * 一般会使用list-style:none让list的标记消失。
  * list-style-position有两个属性值，分别是inside和outside(默认),inside的话，列表会被填充更多的右padding-start，让其整体右移，像缩进去一样。
  
  * 背景样式
  
  
  | 属性 | 复合属性 | 效果 |
  | ---- | ---- | ---- |
  | background | color | 背景颜色 |
  | | image | 背景图片 |
  | | position/size | 图片位置/图片大小 |
  | | repeat | 重复图片的方式 |
  | | origin | 图片定位参照点 |
  | | clip | 图片裁剪 |
  | | attachment | 背景是否固定 |
  
  > 笔记
  * background的position和size都有二个值，水平值和垂直值。当第一个值（水平值确定）而垂直值不定时，垂直值为auto。
  * background的size还可以设置单值，属性值为cover和contain。
  * background的position有x和y是复合属性，而size不是。
  * background的origin和clip的属性值都是content-box、padding-box和border-box
  * background-attachment的属性值是scroll和fixed
  * background可以设置多个背景图像及背景图片相关属性(ie8及以下不兼容)：
  ```css
  .muti-bg-img{
      background-image: url(./bg1.jpg), url(./bg2.jpg); 
      background-position: left top, center center;
      background-repeat: repeat-x, no-repeat;
      background-attachment: fixed, scroll;
  }
  ```
  等价于:
  ```css
  .muti-bg-img{
      background: url(./bg1.jpg) left top repeat-x fixed, url(./bg2.jpg) center center no-repeat scroll;
  }
  ```
  
* 布局样式  

1.浮动

| 属性 | 效果 |
| ---- | ---- |
| float | 浮动 | 
| clear | 清浮动 |
| overflow | 溢出隐藏 |
> 笔记：
* 浮动脱离文档流，不会撑开容器高度，不过可以使用清浮动解决。
* 清浮动样式：

```css
/* 使用伪子类clear清浮动 */
.clearfix::after{
    content: "",
    display: block;
    clear: both;
}
/* 生成BFC清浮动 */
.overfw-bfc{
    overflow: hidden;
}
```

2.定位

| 属性 | 属性值 | 效果 |
| ---- | ---- | ---- |
| position | relative | 相对定位 |
| | absolute | 绝对定位 |
| | fixed | 固定定位 |
| | static | 默认值不使用定位 |
| left | 长度或者% | 相对参照物左边距离 |
| right| 长度或者% | 相对参照物右边距离 |
| top | 长度或者% | 相对参照物上面距离 |
| bottom | 长度或者% | 相对参照物下面距离 |
| z-index | 数值 | 定位堆叠的层级号 |
> 笔记：
* relative相对自身定位，不脱离文档流，占据原来的空间
* absolute相对最近的非static定位的父元素定位，脱离文档流。与浮动不同的是，没有类似清浮动的方法可以使容器高度自适应。
* fixed相对浏览器可视窗口定位
* z-index表示层号，数值大的覆盖数值小的。

* 元素类型和显示

| 属性 | 属性值 | 效果 |
| ---- | ---- | ---- |
| display | block | 块级元素 |
| | inline-block | 行内块元素 |
| | inline | 行内元素 |
| | none | 不显示 |
| | table-cell | 类表格单元格元素 |
| visibility | visible | 元素可见 |
| | hidden | 元素不可见 |
| | collapse | 隐藏表格中的行，非&lt; tr &gt; 表现为hidden|
* display:none和visibility:hidden的区别是前者脱离页面dom树，而后者没有，而且占据空间，影响布局。
* visibilty的hidden和collapse的区别是前者占据空间影响布局，后者会被中下一行元素覆盖，不影响布局

* 弹性盒子

容器：

| 属性 | 效果 |
| ---- | ---- |
| flex-direction | 主轴方向 |
| flex-wrap | 项目换行处理方式 |
| flex-flow | flex-direction flex-wrap的复合简写|
| justify-content | 主轴上项目的对齐方式 |
| align-items | 交叉轴上单行项目的对齐方式 |
| align-content | 交叉轴上多行项目的对齐方式

项目：

| 属性 | 复合属性 | 效果 |
| ---- | ---- | ---- |
| flex | grow | 项目扩大比例 |
| | shrink | 项目缩小比例 |
| | basic | 项目原来占有的空间 |
| order | | 项目排列顺序 |
| align-self | | 单个项目在交叉轴的对齐方式 | 
> 笔记：
* 空间是否剩余和是否不足，由容器大小和项目的basis决定
* grow是剩余空间的划分比例，shrink是空间不足时项目的缩小比例
* 除了空间不足换行，align-seif导致项目与其它项目的交叉轴对齐方式不同，也会出现多行样式
* align-items和align-content的区别在于单行控制和多行控制 [demo](https://codepen.io/maoyonglong/pen/KrgXRv)
* 参考http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html


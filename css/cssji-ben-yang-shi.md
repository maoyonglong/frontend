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
* box-sizing有两个属性值：border-box和content-box，分别表示border限定的盒子大小不变（自动改变元素内容盒子大小来适应）和表示元素内容盒子大小不变。
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
| word-break | | 非CJK单词断行方式 |
| word-wrap | | 长单词（如url）换行方式 |
> 笔记：
* letter-spacing和word-spacing用于处理间距
* text-align有justify属性值，表示两端对齐，这时，可以用text-justify来设置两端对齐的处理方式
* 一行显示不完文本，末尾添加省略号显示的方法：

```css
.ellipsis{
    white-space: nowrap; /*不换行*/
    overflow: hidden; /*溢出隐藏*/
    text-overflow: ellipsis; /*溢出文本显示省略号*/
}
```

* 表格样式





# HTML的语义化标签
>以下默认样式如非特别表现的样式，均写为无。 

* 结构标签

| 标签 | 语义 |
| ---- | ------- |
| &lt; header &gt; | 文档内容头部 |
| &lt; nav &gt; | 导航栏 |
| &lt; main &gt; | 主要内容 |
| &lt; section &gt; | 文档章节或者说是一个内容区域 |
| &lt; article &gt; | 独立的文档内容区域 |
| &lt; aside &gt; | 独立的区块，一般为侧边栏 |
| &lt; footer &gt; | 文档的尾部 |

> 笔记：
* article标签定义独立的文档内容，它往往具有header、footer等部分，也就是它是一个独立完整的文档。比如，博文、新闻、内嵌页面等。
* aside标签定义独立的区块，它不是独立完整的文档，但是由独立于目前的html文档的其它内容，更多地作为一种补充。比如，侧边栏，客服，广告。

* 文本标签

| 标签 | 语义 | 默认样式 |
| ---- | ---- | ---- |
| &lt; strong &gt; | 表示文本强调 | 加粗 |
| &lt; em &gt; | 表示文本强调 | 斜体 |
| &lt; mark &gt; | 表示文本强调 | 黄色字体 |
| &lt; sub &gt; | 文本标号 | 文本下标 |
| &lt; sup &gt; | 文本标号 | 文本上标 |
| &lt; address &gt; | 联系方式 | 无 |
| &lt; time &gt; | 时间 | 无 |
| &lt; small &gt; | 文本旁注 | 小型文本 |
| &lt; cite &gt; | 文章等引用和参考 | 无 |
| &lt; q &gt; | 语句引用 | 添加双引号 |
| &lt; blockquote &gt; | 长语句引用 | 前后添加换行和边距 |
| &lt; del &gt; | 移除的内容 | 文本有删除线 |
| &lt; ins &gt; | 插入的文本 | 文本有下划线 |
| &lt; code &gt; | 一行代码 | 代码格式不变 |
| &lt; pre &gt; | 多行代码 | 代码格式不变 |
> 笔记：
del和ins标签应该一起使用，以显示更换前后的文本

* 功能标签（含特殊属性和功能的标签）

| 标签 | 语义 | 功能 | 默认样式 |
| ---- | ---- | ---- | ---- |
| &lt; attr &gt; | 缩写文本 | 缩写文本 | 鼠标覆盖悬浮显示全文本 |
| &lt; a &gt; | 超链接 | 链接跳转 | 蓝字和下划线 |
> 笔记：
* attr标签使用title定义显示的全文本，标签之间的文本是缩写文本
* a标签使用href定义跳转的链接

* 工具标签


1.表格

| 标签 | 语义 | 默认样式 |
| ---- | ---- | ---- |
| &lt; table &gt; | 表格 | 无 |
| &lt; thead &gt; | 表格头部 | 字体垂直水平居中 |
| &lt; tbody &gt; | 表格内容主体 | 字体垂直居中 |
| &lt; tfoot &gt; | 表格尾部 | 字体垂直居中 |
| &lt; tr &gt; | 表格内容行 | 无 |
| &lt; th &gt; | 表格标题单元格 | 粗体 |
| &lt; td &gt; | 表格单元格 | 无 |
> 笔记：
* 表格结构

```html
<table>
    <thead>
        <tr>
            <th></th> 
        </tr>
    </thead>
    <tbody>
        <tr>
            <td></td>
        </tr>
    </tbody>
    <tfoot>
        <tr>
            <td></td>
        </tr>
    </tfoot>
</table>
```
> th、tr、td可以是多个。
* 使用单元格的colspan、rowspan属性可以实现跨行和跨列。

2.表单

| 标签 | 类型 | 语义 | 默认样式 |
| ---- | ---- | ---- | ---- |
| &lt; form &gt; |  | 表单 | 无 | 
| &lt; fieldset &gt; | | 表单组合域 |  |
| &lt; legend &gt; | | 表单组合域的标题 | |
| &lt; label &gt; |  | 标记 | 无 |
| &lt; input &gt; | text | 单行文本输入框 | 聚焦高亮，下同 |
| | email | 地址输入框 | | 
| | password | 密码输入框 | 输入文本变圆圈 |
| | search | 搜索输入框 | 浏览器差异 |
| | tel | 电话号码输入框 | |
| | url | url输入框 | | 
| | button | 普通按钮 | |
| | submit | 提交按钮 | |
| | reset | 重置按钮 | |
| | image | 图片按钮 | |
| | file | 文件选择器 | |
| | radio | 单选框 | 可选圆点 |
| | checkbox | 复选框 | 可选方框 |
| | number | 数字输入框 |  |
| | range | 滑块 | 滑块条 |
| | datetime-local | 日期时间选择器 | 年月日+时间 |
| | date | 日期选择器 | 年月日 |
| | month | 月选择器 | 月 |
| | time | 时间选择器 | 时间 |
| | week | 周选择器 | 周 |
| | color | 拾色器 | 拾色面板 |
| | hidden | 隐藏内容 | 不可见 |
| &lt; textarea &gt; |  | 多行文本框 | |
| &lt; button &gt; | button(或不写) | 普通按钮 | |
| | submit | 提交按钮 | |
| | reset | 重置按钮 | |
| &lt; select &gt; | | 下拉框 | |
| &lt; datalist &gt; | | 菜单列表 | 下拉菜单列表 | 
| &lt; option &gt; | | 选项 | |
| &lt; progress &gt; | | 进度条 | 单一色进度条 |
| &lt; meter &gt; | | 仪表 | 状态进度条 |
> 笔记：
* 表单元素兼容性查看 [H5表单元素当前状态](https://www.wufoo.com/html5/)
* label标签用于标记其它表单元素，多与input联用，使用for和关联的input的id对应。组合方式一般是:

```html
<label for="form-el1-id">标记：<input id="form-el1-id" /></label>
<label for="form-el2-id">标记：</label><input id="form-el2-id" />
```
> * form的action属性确定提交路径，method属性确定提交方式（GET和POST）  
* 表单元素使用name属性绑定提交时的字段，使用value属性绑定对应的值
* 文本域(input作为输入框和textarea)时，使用placeholder添加提示文本
* input、select和textarea元素都有required属性，表示必须填写字段
* 表单元素都有disaled属性，input（输入框时）和textarea有readonly属性。前者表示不可用，不提交；后者表示只读，值不可更改，提交。
* input文本域（输入框）具有pattern属性，用于使用正则表达式校验文本。

3.多媒体和嵌入元素

| 标签 | 语义 | 
| ---- | ----- |
| &lt; figure &gt; | 独立流内容区域（一般指插图）|
| &lt; figcaption &gt; | figure的标题 |
| &lt; img &gt; | 图片 |
| &lt; audio &gt; | 音频 |
| &lt; video &gt; | 视频 |
| &lt; track &gt; | 歌词或字幕 |
| &lt; iframe &gt; | 内嵌网页 |
| &lt; embed &gt; | 嵌入多媒体（一般是falsh）|
| &lt; object &gt; | 嵌入多媒体（一般是pdf）|
| &lt; param &gt; | object标签的参数 |
> 笔记：
1. track标签兼容性不太好；在移动端，屏幕放大可能会消失。
2. video和audio标签都有autoplay、controls、loop、muted、preload、src属性。其中，前四者是绝对真值，不需要赋值，只要出现就表示应用该属性；preload设置载入情况、src是媒体路径




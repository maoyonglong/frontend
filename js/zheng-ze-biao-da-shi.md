# 正则表达式

## 一、前言
正则表达式是用于**匹配字符串**中字符组合的模式。

## 二、相关方法
在js中，可以使用正则表达式的方法有RegExp对象的exec和test；String对象的match、replace、search和split；

## 三、重要的特殊字符
在正则表达式中通过字符配合特殊字符书写匹配模式。

| 字符 | 含义 |
| --- | --- |
| \ | 转义 |
| ^ | 字符串开头 |
| $ | 字符串结尾 |
| * | 匹配0次或多次 |
| + | 匹配1次或多次 |
| ? | 匹配0次或1次 |
| . | 除换行符以外的任意字符 |
| () | 分组 |
| &#124; |  或 |
| {n} | 匹配n次 |
| {n, m} | 匹配x次， x ∈ [n, m] |
| [xyz] | 字符集，表示匹配里面的任意字符 |
| \[^xyz\] | 方向字符集，表示匹配不在里面的任意字符 |
| \d | 匹配数字 |
| \w | 匹配单字（字母、数字和下划线）|
| \b | 匹配单词边界 |
| \D | 匹配非数字 |
| \W | 匹配非单字 |
| \B | 匹配非单词边界 |

## 四、重要的正则表达式标志
| 标志 | 描述 |
| --- | --- |
| g | 全局搜索 |
| i | 不区分大小写 |
| m | 多行搜索 |
> 笔记：
> 全局模式下，每次开始尝试匹配字符串的开始位置不同。它是依靠lastIndex来定义开始位置的，lastIndex总是等于当前开始匹配的位置的下标。

## 五、特殊的匹配模式
<>区分字符表达方式。比如&lt; + &gt; &lt; - &gt;表示可以使用+也可以使用-

| 字符 | 模式 | 作用 |
| --- | --- | --- |
| 任意量词 | 贪婪模式 | 尽可能多的匹配字符 |
| 任意量词(*+{n}等)加? | 非贪婪模式 | 尽可能少的匹配字符 |
| x(?=y) | 正先行断言 | 当x后面紧跟着y时，才匹配x |
| x(?!y) | 负先行断言 | 当x后面不紧跟着y时，才匹配x |
| (x) | 分组捕获 | 比如，/(foo) (bar) \1 \2/匹配结果中的第一第二个分组；而在替换阶段使用$n代替\n，比如'bar foo'.replace( /(...) (...)/, '$2 $1' ) |
| (?：x) | 非分组捕获 | 比如，/(?:foo){1,2}/匹配(foo)1到2次 |
| （?&lt; name &gt;x）| 命名分组捕获 | 将x匹配分组命名为name |

## 六、方法使用例子
* ###test
test用于测试字符串是否匹配某个正则表达式
```js
// 非全局模式
var str = 'hello world!';
var result = /^hello/.test(str);
console.log(result); // true  
// 全局模式
var regexp= /world/g;
console.log(regexp.lastIndex); // 0
result = regexp.test(str);
console.log(result); // true
console.log(regexp.lastIndex); // 11
result = regexp.test(str);
console.log(result); // false
console.log(regexp.lastIndex); // 0
```
* ###exec
exec用于获取匹配的字符串
```js
// 非全局模式
var re = /quick\s(?<browns>brown).+?(jumps)/i;
var result = re.exec('The Quick Brown Fox Jumps Over The Lazy Dog');
/** result的内容
[
    "Quick Brown Fox Jumps", // 完全匹配字符串
    "Brown", "Jumps", // 分组捕获到的字符串
    index: 4, //完全匹配字符串匹配的开始位置
    groups: {browns: "Brown"} // 命名捕获分组
    input: "The Quick Brown Fox Jumps Over The Lazy Dog" // 原始字符串
    length: 3 // 数组长度
]
*/
// 全局模式
var re = /quick\s(?<browns>brown).+?(jumps)/ig;
var result = re.exec('The Quick Brown Fox Jumps Over The Lazy Dog');
/** result的内容
[
    "Quick Brown Fox Jumps", // 完全匹配字符串
    "Brown", "Jumps", // 分组捕获到的字符串
    index: 4, //完全匹配字符串匹配的开始位置
    groups: {browns: "Brown"} // 命名捕获分组
    input: "The Quick Brown Fox Jumps Over The Lazy Dog" // 原始字符串,
    length: 3 // 数组长度
]
*/
/** re的内容
{
    lastIndex: 25, // 下一次匹配开始位置
    global: true, // 使用全局匹配
    ignoreCase: true, // 忽略大小写
    multiline: false, // 不使用多行匹配
    source: "quick\s(?<browns>brown).+?(jumps)" // 模式字符串
}
*/
```
> 笔记：
> 上面的例子中，exec的全局和非全局模式匹配结果一样，然而不同的是全局模式匹配时，存在着lastIndex改变匹配开始位置。
* ### match
match用于获取匹配的字符串，它与exec具有相同的地方，又有不同的地方，不同的地方在全局模式匹配。
```js
// 非全局模式参照exec，这里略
// 全局模式
var regexp1 = /abc/g; // 不分组捕获
var regexp2 = /abc(d)/g; // 分组捕获
var str = "abcdefgabcdefg";
var eResult1 = regexp1.exec(str); 
var mResult1 = str.match(regexp1);
var eResult2 = regexp2.exec(str); 
var mResult2 = str.match(regexp2);
/** eResult1的内容
[
    "abc", 
    "index" : 0,
    "groups" : undefined,
    "input": "abcdefgabcdefg",
    "length": 1
]
*/
/** mResult1的内容
[
    "abc",
    "abc",
    "length": 2
]
*/
/** eResult2的内容
[
    "abcd",
    "d",
    "index": 0,
    "groups": undefined,
    "input": "abcdefgabcdefg",
    "length": 2
]
*/
/** mResult2的内容
[
    "abcd",
    "abcd",
    "length": 2
]
*/
```
> 笔记：
> 在全局模式下，match不再和exec一致，而是返回一个普通的数组，数组是由全局中所有完全匹配的字符串组成的，也就是说它忽略了分组情况，并自动将所有整个字符串匹配了一遍，不再需要手动重复依靠lastIndex定位匹配。
* ### search
search用于返回匹配位置的下标
```js
var str = "hey JudE";
var re = /[A-Z]/g;
var re2 = /[.]/g;
console.log(str.search(re)); // returns 4, which is the index of the first capital letter "J"
console.log(str.search(re2)); // returns -1 cannot find '.' dot punctuation
```
* ### split
split用于分割字符串
```js
var re = /\s*(?:;|$)\s*/;
var nameList = names.split(re);
console.log(nameList); // [ "Harry Trump", "Fred Barney", "Helen Rigby", "Bill Abel", "Chris Hand", "" ]
```
* ### replace
replace用于替换字符串
```js
var str = 'Twas the night before Xmas...';
var newstr = str.replace(/xmas/i, 'Christmas');
console.log(newstr);  // Twas the night before Christmas...
```
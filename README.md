# css和less 开发规范

这里介绍了css和less的开发规范，让团队的代码风格统一。有利于项目的开发和维护。

在线阅读：http://hongxiyu.github.io/css-and-less-code-styles.


# css

## css结构

###base.css
>主要是对浏览器的一些默认样式进行css reset。

###common.css
>各种模型库，主要定义各种通用样式。
如：
`.bg-left{ float:left }`。

###***.css
>每个页面或者每个专题共用一个独立的css样式，一个css样式文件通常一个人维护。

###***.min.css
>压缩每个专题的css到一个文件，只在页面中引入一个css文件。可以使用gulp或者less进行压缩。

## css书写要求


* 格式
* 注释
* 声明顺序
* a标签伪类书写顺序
* 不要使用@import
* 简写形式的属性声明
* 非必要的情况下，不要给标签写属性
* 清除浮动
* IE css hack
* class 命名
* 其他

### 格式

* 缩进用2个空格
* 每一条规则的大括号 { 前添加空格
* 属性名的`：`后**必须**有空格
* 多个selector共用一个样式集，则多个selector必须**换行**
* 对属性值为0的情况省略单位，如`margin: 0;`
* 对于属性值和颜色参数，省略小于1的小数前面的0 ，如`.6`代替`0.6`,`.5px`代替`0.5px`
* 十六进制值应该全部**小写**，例如`#fff`。（小写的字符易于分辨，因为他们的形式更易于区分）
* 一致使用双引号，如`content: ""`
* 在选择器中以引号夹注属性值，例如：`input[type="checkbox"]`
* 每一个以逗号分隔的属性的逗号后面**不要**保留一个空格

如:

```
.bg {
  margin: 0;
  color: #333;
  background: rgba(0,0,0,.8);
}
```

### 通用

浮动：向左，向右
展现：显示，隐藏


### 声明顺序

相关的属性声明应当归为一组，并按照下面的顺序排列：

1. positioning （定位）
2. box model（盒模型）
3. typographic （排版）
4. visual

由于定位(positioning)可以从正常的文档流中移除元素，并且还能覆盖盒模型(box model)相关的样式，因此排在首位。盒模型排在第二位，因为它决定了组件的尺寸和位置。

其他属性只是影响组件的内部（inside）或者是不影响前两组属性，因此排在后面。

完整的属性列表及其排列顺序请参考 [Recess](http://twitter.github.io/recess/)。

```
#bg {
  /* positioning */
  position: absolute;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;

  /*box model*/
  z-index: 33;
  display: block;
  float: left;
  width: 100px;
  height: 100px;
  max-width: 100%;
  max-height: 100%;
  padding: 30px;
  margin: 10px;
  margin-left: 2px;

  /*typographic*/
  font-size: 30px;
  line-height: 1.3;
  color: #eee;
  text-align: center;
  vertical-align: middle;

  /*visual*/
  background-color: #eee;
  border: 1px solid #fed;
  border-radius: 5px;

  /*misc*/
  opacity: 0.5;
}

```

### 不要使用@import

与`<link>`标签相比，`@import` 指令要慢很多，不光增加了额外的请求次数，还会导致不可预料的问题。替代办法有以下几种：
* 使用多个`<link>`元素
* 通过css预处理器，将多个css文件编译为一个文件，如less或sass

>在这里，我们一般采用第二种方法。

### 简写形式的属性声明

简写属性有：

* padding
* margin
* font
* background
* border
* border-radius

使用规则：
1. 在**不覆盖样式值**的情况下，应该使用简写形式的属性声明值，包括(仅仅设置左右，或者仅仅设置上下，这样修改可以方便很多)
2. 如果只是需要声明其中之一，如`margin-left`,则不使用简写形式。

### a标签伪类书写顺序

>按照`a:link`, `a:visited`, `a:hover`, `a:active` 的顺序，否则在某些浏览器中会失效。

* 在css定义中，`a:hover`必须被置于`a:link` 和 `a:visited`之后，才是有效的。
* 在css定义中，`a:active`必须被置于`a:hover`之后，才是有效的。


### 不要直接对标签写属性

如，`<p class="title">hello bigertech</p>`,设置p字体大小为18px
正确写法：
```
.title {
    font-size: 18px;
}
```
不推荐写法：
```
p {
    font-size: 18px;
}
```


### 清除浮动

>清除浮动**不要**在html中加入标签来清理浮动，通过在浮动元素的**父元素**上添加`.bg-clearfix`来清除浮动

### IE css hack

```
/* 针对ie的hack */
 selector {
    property: value;     /* 所有浏览器 */
    property: value\9;   /* 所有IE浏览器 */
    property: value\0;   /* IE8 */
    +property: value;    /* IE7 */
    _property: value;    /* IE6 */
    *property: value;    /* IE6-7 */
 }
```

>尽量避免使用css hack

### id和class 命名

> * 全都使用**小写**，采用`-`对class中的字母进行分隔,**并且使用bg前缀**。
* 使用ID和类名尽可能短。

这样有助于代码的可理解性和效率。

正确写法：
```
.bg-title {
    font-size: 16px;
}
#nav {}
.author {}
```
不推荐写法：
```
.bgTitle {
    font-size: 16px;
}
#navigation {}
.atr {}
```

### 其他

* 尽量少的使用 !important


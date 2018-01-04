## 前端面试题目汇总

### html
#### 1. html和xhtml有什么不同？
> * HTML是一种基本的WEB网页设计语言，XHTML是一个基于XML的置标语言
> * 最主要的不同：
> * XHTML 元素必须被正确地嵌套。
> * XHTML 元素必须被关闭。
> * 标签名必须用小写字母。
> * XHTML 文档必须拥有根元素。

#### 2. html5有哪些新特性
> *. HTML5 现在已经不是 SGML 的子集，主要是关于图像，位置，存储，多任务等功能的增加。
> * 绘画 canvas &nbsp;:point_right:&nbsp;[canvas时钟](http://vlvlk.tk:3080/time/clock.html)
> * 用于媒介回放的 video 和 audio 元素
> * 本地离线存储 localStorage 长期存储数据，浏览器关闭后数据不丢失；
> * sessionStorage 的数据在浏览器关闭后自动删除
> * 语意化更好的内容元素，比如 article、footer、header、nav、section
> * 表单控件，calendar、date、time、email、url、search
> * 新的技术webworker, websockt, Geolocation
> * 纯表现的元素：basefont，big，center，font, s，strike，tt，u；
> * 对可用性产生负面影响的元素：frame，frameset，noframes；

#### 3. cookies和localStorage和sessionStorage有什么区别？
> * cookies在在服务器和浏览器之间传递的数据
> * localStorage是本地的存储，可以在页面之间传递数据，数据为永久存储，关闭页面数据不会消失。
> * sessionStorage也是本地存储，但是不能在页面之间传递数据，并且关闭页面数据会消失。

#### 4. 同源策略的判断条件是什么？


### js


### css
#### 1. css元素的分类
> 块级元素： div  p  h1  form  ul  li
> 行内元素： span  a  label  input  img   strong  em

#### 2. 隐藏元素的几种方法

> * display: none      在页面内不占用位置
> * visible: false     在页面内占用位置
> * opacity: 0         淡化到看不见，占据页面位置
> * position      必要情况下，可以把元素定位到页面以外，这样看起来就是隐藏了。

#### 3. 页面清除浮动的方法
> * 添加新元素，使用clear: both的特性清除浮动
> * 父级元素定义 overflow: auto(zoom: 1)
> * 伪类:after

* 第一种
```css
.clear{
   clear:both; 
   height: 0; 
   height: 0; 
   overflow:hidden;
}
```
* 第二种
```css
.over-flow{
    overflow: auto; 
    zoom: 1; //处理兼容性问题
}
```
* 第三种
outer是父元素
```css
.outer {zoom:1;}    /* for IE6/7 Maxthon2  */
.outer :after {
   clear:both;
   content:'.';
   display:block;
   width: 0;
   height: 0;
   visibility:hidden;
}
```

#### 4. css如何实现水平居中
>内联元素
- 设置text-align: center
>块级元素
- margin: 0 auto

#### 5. css如何实现垂直居中
> 内联元素

在父元素高度确定的情况下
- 单行文本 父元素设置 height=line-height
- 单行文本 父元素设置 上下padding设置等值
- 多行文本 display: table-cell  vertical-align: middle
        <!-- - 多行文本 display: table vertical-align: middle -->
> 块级元素
- 使用flexbox实现居中
```css
.parent { display: flex; flex-direction: column; justify-content: center; }
```
- 利用transform，在不知道高度的情况下
```css
.parent { position: relative; } .child { position: absolute; top: 50%; transform: translateY(-50%); }
```
参考: [css中各种居中方法](https://www.w3cplus.com/css/centering-css-complete-guide.html)

#### 6. 简单介绍一下sass或者less
> scss: 和less一样是css的预处理语言。
>- scss最重要的一个特性就是能够将css定义成变量，进行复用。
>- 选择器和属性可以嵌套使用，增强了代码的可读性。
>- Mixins可以将一部分样式抽出，作为单独定义的模块，被很多选择器重复使用。
>- 继承选择器的样式

#### 7. 简单介绍一下css盒模型
> 内容(content)、填充(padding)、边框(border)、边界(margin)， CSS盒子模式都具备这些属性。
> 比较特别的是有个css的属性叫做box-sizing。 
> * 当box-sizing: content-box： 为元素设置的内边距和边框向外扩展，不算入content之内
> * 当box-sizing: border-box: 为元素设置的内边距和边框向内扩展，算在content之内。

#### 8. 说一下css3的新特性
> 圆角（border-redius） 阴影（box-shadow）文字阴影( text-shadow)

> 渐变（gradient） 旋转（transform）

一般情况下，使用border-box时，调整内边距和边框的宽度不会影响页面的布局。

### 框架的理解


### es6


### http and http2


### 前端规范


### 算法


### nodejs
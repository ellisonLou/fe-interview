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
> * 所谓的同源策略，指的是**域名**、**协议**、**端口**相同，javascript脚本才会被执行，不然浏览器会报错。非同源资源请求被称作是**跨域**。

#### 5. 如何实现跨域请求？
> * 利用jsonp实现。jsonp的实现原理实际上利用了`<script>`标签没有同源限制的漏洞，在传递的请求中加入了callback。前端只需要处理此callback带回的数据即可。比如说像这样：
```js
<script src="http://www.example.net/api?param1=1&param2=1"></script>
```
jsonp缺点是只能进行get请求，而不能进行post请求。

> * document.domain + iframe 。这个方法只能在有相同的基础域名的情况下才能成功。比如a.host.net嵌套了一个b.host.net的iframe。将a.host.net设置成document.domain="host.net",将b.host.net设置成document.domain="host.net"，那么a.host.net和b.host.net就不受同源限制了。

> * cors（Cross Origin Resourse Share）实现cors的关键在于服务器，只要服务器实现了cors的接口，那么在前端写起来和普通的js没有区别。
&nbsp;:point_right:&nbsp;&nbsp;[阮一峰-详细解释cors](http://www.ruanyifeng.com/blog/2016/04/cors.html)
cors比jsonp强大很多，它支持post请求，缺点是不支持cors的服务器无法请求。

> * 服务器代理，简单来说就是浏览器不可以跨域请求，但是服务器可以跨域请求（通过http-proxy-middleware代理或者http模块请求）

#### 6. 浏览器渲染原理解析
&nbsp;:point_right:&nbsp;&nbsp;[浏览器是如何工作的：隐藏在页面背后的原理](https://www.html5rocks.com/en/tutorials/internals/howbrowserswork/)


#### 5. doctype是什么？
[mdn链接，解释doctype](https://developer.mozilla.org/en-US/docs/Web/HTML/Quirks_Mode_and_Standards_Mode)
中文稍后再补充。


### js
#### 1. 什么是原型链


#### 2. 请说一说事件模型
> dom事件流包括三个阶段，
> 1. 事件捕获阶段： 事件开始由顶层对象触发，然后逐渐向下传播，直到目标元素。
> 2. 处于目标阶段： 事件处于绑定的元素上。
> 3. 事件冒泡阶段： 事件由目标元素接收后，逐渐向上传播，直到不知名元素。
> * 问题1： 如何阻止事件冒泡？  event.stopPropagation()

#### 3. 闭包
请参考博客

#### 4. instanceof 和 typeof的区别
> * typeof
```js
typeof undefined == 'undefined'
typeof null == 'object'
typeof true == 'boolean'
typeof 'a' == 'string'
typeof function() {} == 'function'
typeof 3.14 == 'number'
```

> * instanceof
instanceof 的原理其实和原型链相关，具体请查看博客：  
```js
var C = function() {}
var o = new C();
o instanceof C  //true    // C.prototype在o的原型链上
o instanceof Object //true  // Object.prototype在o的原型链上

C.prototype = {}
o instanceof C;  // flase  C.prototype指向空对象，从o的原型链上消失。

var D = function() {};  // 继承
D.prototype = new C();
var d = new D();
d instanceof C;  // true
d instanceof D;  // true
```

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

#### 9. 说说重排和重绘
&nbsp;:point_right:&nbsp;&nbsp;[阮一峰-重排和重绘](http://www.ruanyifeng.com/blog/2015/09/web-page-performance-in-depth.html)


#### 10. 页面适配问题（移动端）
> * 一种方案就是通过判断移动端和pc端，服务器给出不同的页面，分开处理。
> * 通过设置viewport适配大部分移动端屏幕分辨率


#### 11. BFC的生成条件
> * overflow不是visible以外的所有值
> * float 不是none之外的所有值
> * display: inline-block table-cell table-caption
> * position: absolute 或者 fixed

总结一下，就是所有脱离文档流的布局，其都会产生BFC，再加上overflow非visible和display: inline-block table-cell table-caption
根据w3, css level 2 里把这个叫做： ```containing block is established differently.``` 
css level 3 里面叫做 flow root

#### 12. css盒子模型
1. block boxes
display: block | table | list-item会让元素变成块级元素。块级元素具有如下特点：
    - 可以使用height,width,padding，margin
    - 每一个块级元素占据一行

2. inline boxs
display: inline | inline-block | inline-table

3. inline block
display: inline-block
A block box, which itself is flowed as a single inline box, similar to a replaced element. The inside of an inline-block is formatted as a block box, and the box itself is formatted as an inline box.

#### 13. line-hight
>  为一个盒子设置line-hight实际上是为这个盒子里面所有的line-box设置高度。而文字在一个line-box中一定是居中显示的。这就是内联元素设置line-height等于父元素高度可以居中的原因。
>  同时，在父元素中设置行高和在父元素的内联元素中设置行高(line-hight是一样的)，如下：
```html
<div style="height: 100px; line-hight: 100px;">
    <span>Hello</span>
</div>
```
```html
<div style="height: 100px;">
    <span style="line-hight: 100px">World</span>
</div>
```
这两个都一样，都可以实现span里面元素的居中。原理就是无论line-hight在span上还是在span上，它都作用于


#### 12. 说说BFC的规则。
> * 内部box从上到下一个一个放置。
> * 垂直方向的距离由margin决定。
> * 每个元素的左外边距和包含快的左边距接触。
> * BFC区域不会和float元素重叠。
> * BFC里面的float元素也会参与高度的计算。
> * BFC是页面上的一个独立的元素，不会影响到其它元素。
> * BFC上下相邻两个元素会发生外边距重叠。


#### 13. 使用伪元素清除浮动的原理是什么？
clearfix的源代码
```css
.clearfix:before,
.clearfix:after {
    content: '.';  /* 生成内容作为最后一个元素 */
    display: block;  /* 使生成的元素以块级显示，占满剩余空间 */
    height: 0;  /* 为了不改变原来的文档流 */
    visibility:hidden;  /* 使生成的内容不可见 */
}
.clearfix {
    clear: both;
}
.clearfix {
    zoom: 1; /* 触发ie的hasLayout */
}
```


#### 14. 使用overflow: auto清除浮动的原理是什么？
> 答： 父级元素使用overflow: auto会创建BFC(Block Format Context),在计算BFC的高度时，浮动的子元素也会参与计算，因此overflow: auto可以用来作为清除浮动。

#### 15. BFC如何防止嵌套元素外边距重叠
> * 外边距折叠之父子外边距折叠，解决方法就是在父级形成BFC即可。
> * 兄弟元素外边距折叠。

#### 16. 列表化排版的几种方式
> * 浮动是魔鬼
张鑫旭大神说了，到目前为止，无论是分栏布局还是列表排列，都可以用其它的方法代替浮动(float: left | right| none)。

> * display: inline-box

> * 

### 网络相关
#### 1. web 性能优化的理解
减少http请求
> * 合理设置缓存可以有效减少http请求。图片之类长时间不变的资源可以通过Expires设置很长的过期时间。
> * 通过压缩css,js等。将多个css，js压缩成一个文件，将图片做成雪碧图。
> * 利用localStorage缓存logo,js，css等，一般可以设置数天的时间。
> * 服务器采用Gzip压缩。（对服务器影响较大）。
> * 图片lazy load.

操作dom和写javascript代码时考虑性能问题。
> * 少用全局变量，减少作用域链查找。
> * 缓存dom查找结果。
> * 使用闭包时考虑内存泄漏问题。

使用cdn加速
> * 一般cdn服务商到用户的距离在路由器上转发的次数是最少的，静态资源可以放在cdn上，不仅减轻了总服务器的压力，还能加速网页请求的时间。

使用反向代理服务器
> * 启用反向代理服务做请求的转发，能够减轻每一个服务器的负担

#### 2. Tcp三次握手简述
> 首先客户端发送SYN, 服务器收到后返回SYN/ACK, 客户端接收到返回后，继续发送ACK,服务器接收到，三次握手成功。如果其中有一步失败，则进行重新三次握手。

#### 3. http2 比http1.1改进了哪些地方
> * 采用二进制协议，解析更加高效
> * 多路复用（Multiplexing），在一条Tcp连接上可以进行多次请求，不会有http1.1请求拥塞的问题。
> * server push(服务器主动传递数据到客户端)

#### 4. http请求中的etag是什么？
etag和if-none-match配合用来做缓存。流程如下：
1. 客户端请求一个资源，服务器返回该资源并在上面生成一个etag,返回给客户端。
2. 客户端缓存该服务器返回的e-tag。
3. 客户端第二次请求中,header中带上了一个字段名为if-none-match，实际值就是e-tag的值，服务器根据该值判断是否使用缓存资源。




### 框架的理解
#### 1. 组件化的理解
> 组件化有几个优点
> * 可重用： 简单并且功能清晰的组件，可以被很多更大的组件复用
> * 可维护： 组件化有利于代码的解耦，对一个组件代码的改动不会影响到其他组件。

#### 2. vue.js
> * 组件生命周期

beforeCreated 组件实例刚被创建，组件属性计算之前，data
created 组件属性被绑定，但是dom还未生成
beforeMount 模板编译、挂载之前
mounted 模板编译、挂载之后
beforeUpdate 组件更新之前
updated 组件更新之后
beforeDestory 组件卸载之前
destoryed 组件卸载之后
activated 组件被激活时调用
disactivated 组件被移除时调用

> * 组件之间的数据传递
vue通过props向子组件传递数据。通过events向父组件传递数据。

> * vue-router的使用

> * 有没有使用过vuex，对vuex有什么理解，有没有尝试阅读源代码？

> * vuex数据双向绑定的原理？

> * vue如何实现非父子关系组件通信
通过vuex可以解决这个问题。

#### react.js

### 框架的理解


### es6




### 前端规范


### 算法


### nodejs
# CSS+HTML
## HTML
### 回流和重绘
#### 回流
> 当页面中的元素大小改变、元素隐藏/显示、添加边框、padding、margin等改变需要重新布局
#### 重绘
> 当页面中的元素某些属性改变，如background-color 便会引起重绘
#### 区别
* 回流必将引起重绘
* 重绘不一定引起回流
### BFC
> 块级格式化上下文
#### 如何触发
* 根元素，即html
* float的值不为none（默认） 
* overflow的值不为visible（默认）
* display的值为inline-block、table-cell、table-caption 
* position的值为absolute或fixed
### 盒子模型
* 标准版  
> 宽度=内容的宽度(content)+border+padding+margin  
* ie的盒子模型
> 宽度=内容的宽度(content+border+padding)+margin
### css尺寸
| 单位 | 性质 | 描述 |
| :---: | :---: | :---: |
|px|绝对单位|像素,屏幕上的一个点|
|rpx|相对单位|...|
|em|相对单位|相对于父元素字体的尺寸,一般浏览器字体大小默认为16px,2em==32px|
|rem|相对单位|相对于根元素(html)的font-size来计算|
|vw|相对单位|相对于视口的宽度,视口被分成100份|
|vh|相对单位|相对于视口的高度,视口被分成100份|
* 建议微信小程序设计师按照iphone6的屏幕来设计小程序, 设计图宽度为750px, 这样开发的时候, 直接用设计图上量出来多少px, 开发中就是多少rpx 
> rpx,微信小程序中的单位  
>> 根据屏幕宽度和物理像素计算  
>> eg:iphone6 屏幕宽度为375px 共有750个物理像素,则1rpx=0.5px

快捷导航:[移动端web开发的设计稿和工作流](https://juejin.im/post/5c072b586fb9a049f06a09e7)
### css初始化
> 原因: 浏览器兼容性问题，不同浏览器的不同的标签， 默认属性值不同
```css
*{
	box-sizing:border-box;
	-moz-box-sizing:border-box;/*兼容低版本的浏览器*/
	-webkit-box-sizing:border-box;/*为了兼容低版本的web*/
	color:#000;
}
body{
	font-size:12px;
	font-family:Arial,Verdana,Tahoma,"微软雅黑","黑体";
	line-height:120%;
	background:#fff;
	margin:0;
	overflow-x:hidden;/*溢出隐藏，去掉水平方向的，直接剪裁*/
}
p,h1,h2,h3,h4,h5,h6,ul,ol,dl,li,form,table{
	margin:0;
	padding:0;
}
a,img{
	border:none;/*兼容ie浏览器*/
}
img{
	vertical-align:middle;
	border:0;
}
li{
	list-style:none;
}
i,em{
	font-style:normal;
}
a{
	text-decoration:none; 
	color:#000000;
	border:0;
}
a:link{
	text-decoration:none; 
	color:#000000;
}
a:visited{
	text-decoration:none; 
	color:#000000;
}
a:hover{
	text-decoration:none; 
	color:#000000;
}
a:active{
	text-decoration:none; 
	color:#000000;
}
.clearfix:before,.clearfix:after{
	display:table;
	content:"";
}
.clearfix:after{
	clear:both;
}
.clearfix{
	*zoom:1;
}/*兼容ie浏览器*/
table{border-collapse:collapse;}
```
### 关于box-sizing
> 用来控制元素的盒子模型的解析模式 默认是content-box
* content-box 是w3c的标准盒子模型 元素的height/width是content的宽高
* border-box IE传统盒子模型  元素的height/width是content+border+padding
### css选择器有哪些，那些可以继承
#### 选择器
* id选择器
* 类选择器
* 标签选择器
* 相邻选择器     +
* 子选择器       >
* 后代选择器     li a
* 通配符选择器   *
* 属性选择器     a[rel="external"]
* 伪类选择器     a:hover   li:last-child
> 优先级
>> !important>[id>class>tag]
>>> !important 比内联优先级高
#### 可继承的属性
* font-size
* font-family
* color
#### 不可继承的属性
* border
* padding
* margin
* width
* height
### position
* static 默认 按照文档流排列
* relative (相对定位) 不脱离文档流  参考自身静态位置
* absolute (绝对定位) 参考最近的一个不为static的父级元素定位
* fixed(固定定位) 参考窗口进行定位
#### 粘性定位
安卓兼容性不太好
* sticky
> sticky 元素仅在父元素中生效  
> 父元素不能是overflow:hidden或者overflow:auto  
> 必须指定四个位置之一 否则是相对定位  
> 父元素高度大于粘性元素的高度  
### css写一个三角形
> 宽高为0 设置边框
```text
div{
    width: 0;
    height: 0;
    border-top: 40px solid transparent;
    border-left: 40px solid transparent;
    border-right: 40px solid transparent;
    border-bottom: 40px solid #ff0000;
}
```
### display:none 和 visibility:hidden
* display:none;  不显示元素，不分配空间(重绘和回流)
* visibility:hidden; 隐藏元素，仍保留原来的空间(重绘)
### 伪元素和伪类
| 伪元素 | 伪类 |
| :---: | :---: |
|是给自己虚拟的元素添加样式;虚拟的，并不存在于DOM|像类选择器一样给已存在某个元素添加额外的样式|
|两个冒号|一个冒号|
|before、after|hover、active、first-child、last-child、nth-child()|
### 浮动
> 浮动元素脱离文档刘
#### 如何清除浮动
* 父级元素定义个height
* 在最后添加一个div 并设置clear:both;
* 父级元素添加样式overflow为hidden或auto
* 父级div定义zoom
* 使用伪元素
```css
/* zoom */
.class{
    *zoom: 1;
}
/* 伪元素(ie8以上) */
.class::after,.class::before{
    content: '';
    display: block;
    height: 0;
    visibility: hidden;
    clear: both;
}
```
#### 设置元素浮动之后，该元素的display属性为block  
### 上下margin重合问题
> 在重合元素外包裹一层容器，并触发该容器的BFC(使重叠的两个盒子分属于两个BFC)
### css预处理器有哪些？
* less
* sass
* Stylus (给node项目做css预处理支持)
### CSS优化
* 避免过度约束
* 避免后代选择符
* 避免链式选择符
* 使用紧凑的语法
* 避免不必要的命名空间
* 避免不必要的重复
* 最好使用表示语义的名字。一个好的类名应该是描述他是什么而不是像什么
* 避免！important，可以选择其他选择器
* 尽可能的精简规则，你可以合并不同类里的重复规则
### 全屏滚动
> 原理：有点类似于轮播，整体的元素一直排列下去，假设有5个需要展示的全屏页面，那么高度是500%，只是展示100%，剩下的可以通过transform进行y轴定位，也可以通过margin-top实现
* overflow：hidden；transition：all 1000ms ease
### 关于line-height
> 行高是指一行文字的高度，具体说是两行文字间基线的距离。CSS中起高度作用的是height和line-height，没有定义height属性，最终其表现作用一定是line-height
* 单行文本垂直居中:把line-height值设置为height一样大小
* 多行文本垂直居中:设置display属性为inline-block
### 怎么让Chrome支持小于12px 的文字？
```css
p{
    font-size:10px;
    -webkit-transform:scale(0.8);
}
```
### 让页面里的字体变清晰，变细用CSS怎么做？
> -webkit-font-smoothing在window系统下没有起作用，但是在IOS设备上起作用-webkit-font-smoothing：antialiased是最佳的，灰度平滑
### position:fixed;在android下无效怎么处理？  
```html
<meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0, user-scalable=no"/>
```
### li与li之间有看不见的空白间隔是什么原因引起的？有什么解决办法？
> 行框的排列会受到中间空白（回车空格）等的影响，因为空格也属于字符,这些空白也会被应用样式，占据空间，所以会有间隔，把字符大小设为0，就没有空格了
#### 解决方法
* 可以将<li>代码全部写在一排
* 浮动li中float：left
* 在ul中用font-size:0; (谷歌不支持) 可以使用letter-space:-3px;
### display:inline-block 什么时候会显示间隙？
* 有空格时候会有间隙 解决：移除空格  
* margin正值的时候 解决：margin使用负值  
* 使用font-size时候 解决：font-size:0、letter-spacing、word-spacing  
### 有一个高度自适应的div，里面有两个div，一个高度100px，希望另一个填满剩下的高度
> 外层div使用position：relative；高度要求自适应的div使用position: absolute; top: 100px; bottom: 0; left: 0
### style标签写在body后与body前有什么区别？
> 写在body标签后由于浏览器以逐行方式对HTML文档进行解析，当解析到写在尾部的样式表（外联或写在style标签）会导致浏览器停止之前的渲染，等待加载且解析样式表完成之后重新渲染，在windows的IE下可能会出现FOUC现象（即样式失效导致的页面闪烁问题）
### CSS属性overflow属性定义溢出元素内容区的内容会如何处理?
* 参数是scroll时候，必会出现滚动条
* 参数是auto时候，子元素内容大于父元素时出现滚动条
* 参数是visible时候，溢出的内容出现在父元素之外
* 参数是hidden时候，溢出隐藏
### Sprites
> 将一个页面涉及到的所有图片都包含到一张大图中去，然后利用CSS的 background-image，background- repeat，background-position 的组合进行背景定位。利用CSS Sprites能很好地减少网页的http请求，从而大大的提高页面的性能；CSS Sprites能减少图片的字节。
###  inline-block空白节点产生原因，怎么消除
* 原因：元素被当成行内元素排版的时候，元素之间的空白符（空格、回车换行等）都会被浏览器处理，根据white-space的处理方式（默认是normal，合并多余空白），原来HTML代码中的回车换行被转成一个空白符，所以元素之间就出现了空隙。这些元素之间的间距会随着字体的大小而变化，当行内元素font-size:16px时，间距为8px
* 消除
    * 去除元素间的空白
    * 父元素设置font-size为0，子元素单独再设置字体大小
    * 设置margin-right为负值
    * 给inline-block元素加float或者flex
    * 设置字符间距或单词间距
### 响应式设计？响应式设计的基本原理是什么？如何兼容低版本的IE？
> 响应式网站设计(Responsive Web design)是一个网站能够兼容多个终端，而不是为每一个终端做一个特定的版本。
  基本原理是通过媒体查询检测不同的设备屏幕尺寸做处理。
  页面头部必须有meta声明的viewport  
> 通过 rem、em、% 实现响应式
```html
<meta name="’viewport’" content="”width=device-width," initial-scale="1.0" maximum-scale="1,user-scalable=no”"/>
```
```text
width  ----  viewport的宽度（width=device-width意思是：宽度等于设备宽度）
height ------  viewport的高度（height=device-height意思是：高度等于设备宽度）
initial-scale ----- 初始的缩放比例
minimum-scale ----- 允许用户缩放到的最小比例
maximum-scale ----- 允许用户缩放到的最大比例
user-scalable ----- 用户是否可以手动缩放
```
### 动画方面
#### 如果需要手动写动画，你认为最小时间间隔是多久，为什么
> 多数显示器默认频率是60Hz，即1秒刷新60次，所以理论上最小间隔为1/60*1000ms ＝ 16.7ms
#### CSS动画和Js动画的区别
##### JS动画
* 优点
    * 可控性强，可以在动画播放的任意过程做操作
    * 动画效果比CSS强，有些动画只有JS才能实现
    * 基本上没有兼容性问题
* 缺点
    * js在主线程中运行，动画会进行干扰导致线程阻塞，造成丢帧
    * 代码复杂度高于CSS
##### CSS动画
* 优点
    * 浏览器可以对动画进行优化(通过GPU提高动画性能)
* 缺点
    * 可控制性弱，只能暂停，不能在动画中寻找到一个特定的时间点做特定的操作
    * 代码冗长，若想要实现稍复杂的动画，CSS代码会变得特别笨重
#### CSS动画有哪些属性
* animation-name                关键帧的名称
* animation-duration            动画的持续时间
* animation-timing-function     动画运用的类型(匀速、加速度、减速度、贝塞尔曲线)
* animation-delay               动画的延迟
* animation-iteration-count     动画运动的次数(默认情况下运行一次/infinite 无限循环)
* animation-direction           运动的方向
    * reverse                   反方向运动
    * alternate                 动画先正常运动再反方向运动，并持续交替运行
    * alternate-reverse         动画先反运行再正方向运行，并持续交替运行
* animation-play-state
    * pause                     暂停
    * running                   运动
* animation-timing-function     动画类型
    * linear
    * ease
    * ease-in
    * step-start                没有动画中间的过渡效果。每次直接跳到下一帧开始的地方 可以做出GIF的效果
* 制作关键帧
```css
@keyframes name {
/*
from{}
to{}   适合动画少的
*/
0%{}        /*开始状态*/
25%{}
50%{}
75%{}
100%{}      /*结束状态*/
}
```

# JS
## 声明提升类问题
* 变量提升
* 函数声明
## 匿名函数
## 原型及原型链
## 闭包及其作用
> closure  闭包由函数引用其词法环境绑在一起形成的组合结构，在js中，闭包在每个函数被创建时形成  
> 闭包与他的词法环境绑定在一起，因此，闭包让我们能从一个函数内部访问外部函数的作用域  
> 使用:在一个函数内定义另外一个函数，并将他暴露出来，要暴露一个函数，可以将它返回或者传给其他的函数  
> 内部函数能访问到外部函数作用域的变量，即使外部函数已经执行完毕  
> 闭包就是将函数内部和函数外部连接起来的一座桥梁
#### 关于作用域
1. 全局作用域
2. 函数作用域
> 函数可以读取全局变量，但是全局无法读取函数中的变量  
> 注意在函数内部声明变量的时候，如果不用var/let等声明，其实是声明了一个全局变量
### 用途
* 实现数据的私有化
> 数据的私有化可以让我们面向接口编程而不是面向实现编程  



## 箭头函数
## this指向(如何确定)
## for循环中的作用域
## 函数式编程
## 事件循环机制 
[参考](https://zhuanlan.zhihu.com/p/33058983)
> 单线程非阻塞、执行栈、事件队列、宏任务(setTimeout()、setInterval())、微任务(new Promise())
## ES6
## Promise 
### 手写Promise
### 怎么实现的
### 执行顺序
[参考](https://es6.ruanyifeng.com/?search=%E7%AE%AD%E5%A4%B4%E5%87%BD%E6%95%B0&x=0&y=0#docs/promise)
### Promise.all要怎么实现
## 页面发了个请求，请求没返回用户就切去另一个页面了，这会有什么影响，怎么处理？fetch请求怎么取消
## 节流和防抖
## 深拷贝
[参考](https://juejin.im/post/5abb55ee6fb9a028e33b7e0a)
## call，apply, bind的区别
## bind怎么实现call
## js存储方式
* cookie
* sessionStorage
* localStorage
* indexedDB
## 跨域
* 跨域怎么产生
* 如何解决跨域
> jsonp跨域、nginx反向代理、node.js中间件代理跨域、后端设置http header、后端在服务器上设置cors
* CORS头设置
* 跨域时身份认证信息怎么携带
## ajax axios fetch
### ajax
> jquery.ajax 提供了jsonp支持
* 优点
    * 原生支持，不需要任何插件
    * 基于XMLHttpRequest 无刷新更新页面
* 缺点
    * 可能破坏浏览器的后退机制
    * 嵌套回调，难以处理
### axios
> 基于XMLHttpRequest 是promise的实现版本
* 优点
    * 支持浏览器和node.js
    * 支持promise
    * 能拦截请求和响应
    * 能取消请求
    * 自动转换JSON数据
    * 浏览器端支持防止CSRF(跨站请求伪造)
### fetch
> 全局 fetch()方法 不基于XMLHttpRequest
* 优点
    * 符合关注分离，没有将输入、输出和用事件来跟踪的状态混杂在一个对象里
    * 更好更方便的写法
    * 更加底层，提供的API丰富（request, response）
    * 脱离了XHR，是ES规范里新的实现方式
* 缺点
    * fetchtch只对网络请求报错，对400，500都当做成功的请求，需要封装去处理
    * etch默认不会带cookie，需要添加配置项
    * fetch不支持abort，不支持超时控制，使用setTimeout及Promise.reject的实现的超时控制并不能阻止请求过程继续在后台运行，造成了量的浪费
    * fetch没有办法原生监测请求的进度，而XHR可以
## js浮点数运算精度问题
[参考](https://blog.csdn.net/helloxiaoliang/article/details/72723387)

## Proxy 与 Object.defineProperty 优劣对比
[参考](https://es6.ruanyifeng.com/#docs/proxy)


## canvas
## canvas和svg的特点和选择


## 手写部分
### 手写$(document).ready
```javascript
    document.ready = function (callback) {
        if (document.addEventListener) {
            document.addEventListener('DOMContentLoaded', function () {
                removeEventListener('DOMContentLoaded', arguments.callee, false);
                callback()
            })
        } else if (document.attachEvent) {
            document.attachEvent('onreadystatechange', function () {
                if (doucment.readyState === 'complete') {
                    document.detachEvent('onreadystatechange', arguments.callee);
                    callback()
                }
            })
        } else if (document.lastChild == document.body) {
            callback()
        }
    };
```
####
* DOM2级事件定义了两个方法用于处理指定和删除事件处理程序的操作：
    * addEventListener
    * removeEventListener
    * 参数
        1. 事件类型
        2. 事件处理方法
        3. 布尔参数，默认false
        (true捕获阶段调用事件处理方法；false冒泡阶段调用事件处理方法。)
* IE不支持addEventListener和removeEventListener方法,但是实现了两个类似的方法：
    * attachEvent
    * detachEvent
    * 这两个方法都接受两个相同的参数。  
        1. 事件处理程序名称  
        2. 事件处理程序方法

# 网络部分
## 浏览器输入url之后发生了什么
### DNS查询
> 若输入的url包含域名，会涉及到DNS解析，若是IP，就不会涉及

    1. 在本地域名服务器中根据域名查询ip
    2. 若没有找到，会向根域名服务器发送请求
    3. 若根域名服务器中也不存在，本地域名会向顶级域名服务器(TLD)发送请求
    4. 以此类推，知道找到后，会在本地缓存ip地址，以备下次使用
    
* 系统缓存
    * Linux     =>   /etc/hosts
    * Windows   =>   C:\Windows\System32\Drivers\etc\hosts
### 建立TCP连接
> DNS返回域名的ip之后，就是浏览器和ip建立TCP连接(HTTP基于TCP)
#### TCP三次握手和四次挥手
##### 三次握手
> 建立TCP连接时，客户端和服务器总共发送3个包  
> 目的： 连接服务器制定端口，建立TCP连接，并同步连接双方的序列号和确认号，并交换TCP窗口大小信息
##### 四次挥手
> TCP连接的拆除需要发送四个包，因此得名
#### HTTPS证书
> 对于https，需要有一个SSL/TLS的鉴权/认证，才能建立TCP连接
### HTTP/HTTPS请求
#### 关于http的10问
* HTTP METHOD有哪几种，分别是什么？

* HTTP的PUT/DELETE/等使用时需要注意什么？
* HTTP的OPTIONS用来做什么？
    * OPTIONS一般用来获取目标资源的通信选项，例如确认允许的HTTP Method [eg](https://developer.mozilla.org/en-US/docs/Web/HTTP/Methods/OPTIONS)
    * 一般用在CORS上
* response里的server哪里不合适，需要注意什么
    * 不应该把server的版本信息放在这里   因为web server每个版本都有安全漏洞
* Status Code 302与307的区别是什么
    * 在 GET、HEAD 这些幂等的请求方式上，302、307 没区别，但对于 POST 就不同了，大部分浏览器 都会 302 会将 POST 请求转为 GET，而 307则不一样，规范要求浏览器继续向 Location 的地址 POST 内容。
    * 举个例子解释一下，假设正在POST一个消息，里面的Body有1M内容，在307的情况下，这1M的内容会继续发过去，但在302的情况下，则不会。
* 在HTTP Response里Connection的用法需要注意什么
    * 优化网络时经常用到
    * 需要注意的是，Connection在通信领域会一些场景下会造成一些麻烦，尤其是在监控某个HTTP Session的flow时
* 在HTTP Response里Strict-Transport-Security（HSTS）怎么用
* 可以抓HTTPS的包了解HTTP请求和响应吗？有什么方法？
    * Fiddler，HTTP Analyzer
* 为什么对性能要求高的场景下不使用HTTP作为协议？例如在商用里，RPC开源项目一般不使用HTTP作为传输协议？而在5G下使用HTTP协议呢？
    * HTTP的消息头太多了，会造成消息体特别大，影响性能，而且有些场景下这些消息头大部分都是无用的
    * 但是在5G里，为什么3GPP组织会采用HTTP协议作为各个reference point的interface的实现
* HTTP协议（包括HTTP/2.0）有了解吗
    * HTTP/2.0还是需要了解一下，优势和缺点
### 浏览器解析和渲染页面
> 浏览器接受server的返回内容 然后呈现  
> 是一个渐进的过程，为了用户体验，浏览器会边解析边渲染，并不会等到HTML解析完了才开始构造和布局渲染树
* 根据 HTML 结构生成 DOM 树
* 根据 CSS 生成 CSSOM
* 将 DOM 和 CSSOM 整合形成 RenderTree
* 根据 RenderTree 开始渲染和展示
* 遇到script标签时，会执行并阻塞渲染
#### 浏览器渲染问题
* 浏览器显示页面的主要流程是什么？
* 渲染引擎是单线程还是多线程？
* 浏览器的网络操作一般由几个线程去执行？
* DOM树，渲染树是什么？
* 为了获得更好的用户体验，我们应该在页面做些什么改进？
* 浏览器是如何打开PDF，Word等文档的？
### HTTP连接断开

### WEB优化
[雅虎的总结](https://developer.yahoo.com/performance/rules.html)
* 不要把layout嵌入一层又一层，简单说就是嵌套别太深，不然影响解析和渲染性能。
* 有些数据可以在后台处理的，就不要在前端通过JavaScript处理了。
* 如果请求过大，Load Balance这些手段还是要上的。
* 保持HTTP连接，合理设置Connection。
* 后台事件性能要高，能够及时将结果返回给用户。
## 状态码
* 1**   服务器收到请求，要求请求者继续操作
* 2**   成功，操作被成功接收并处理
* 3**   重定向，需要进一步操作以完成请求
* 4**   客户端错误，请求包含语法错误或无法完成请求
* 5**   服务端错误，服务端在处理过程中发生错误

# SPA框架
## 为什么选择使用框架而不是原生[参考](https://juejin.im/post/5d5f44dae51d4561df7805b4)
* 组件化
* 天然分层 代码解耦
* 生态链完整
* 开发效率
## 虚拟 DOM 的优缺点
* 虚拟DOM
* 优点
    * 保证性能下限：通过diff，找出最小差异，然后批量进行patch
    * 无需手动操作DOM：虚拟DOM的diff和parch都是在一次更新中自动进行的
    * 跨平台：虚拟DOM本质上是javascript对象，而DOM与平台强相关
* 缺点
    * 无法进行极致性优化：在一些性能要求极高的应用中虚拟DOM无法进行针对性的极致优化,
## 虚拟 DOM 实现原理
## 什么是 MVVM
> 由数据驱动，实现数据的双向绑定
* Model 数据模型
* View UI组件
* ViewModel 同步View 和 Model的对象
## 说说你对 SPA 单页面的理解，它的优缺点分别是什么
> 就是在 Web 页面初始化时加载所有的 HTML、JavaScript 和 CSS，页面的内容的变化，靠动态创建dom
* 优点
    * 用户体验好、快，内容的改变不需要重新加载整个页面，避免了不必要的跳转和重复渲染；
    * 基于上面一点，SPA 对服务器的压力小；
    * 前后端职责分离，架构清晰，前端进行交互逻辑，后端负责数据处理；
* 缺点
    * 初次加载耗时多，为实现单页 Web 应用功能及显示效果，需要在加载页面的时候将 JavaScript、CSS 统一加载，部分页面按需加载；
    * 前进后退路由管理，由于单页应用在一个页面中显示所有的内容，所以不能使用浏览器的前进后退功能，所有的页面切换需要自己建立堆栈管理
    * SEO 难度较大，由于所有的内容都在一个页面中动态替换显示，所以在 SEO 上其有着天然的弱势

## VUE
[面试题](https://juejin.im/post/5d59f2a451882549be53b170)
### 导航守卫
[官方文档](https://router.vuejs.org/zh/guide/advanced/navigation-guards.html)
* 全局钩子
* 路由独享钩子
* 组件内钩子
### 生命周期
#### Vue 的父组件和子组件生命周期钩子函数执行顺序
* 加载渲染过程
    * 父 beforeCreate -> 父 created -> 父 beforeMount -> 子 beforeCreate -> 子 created -> 子 beforeMount -> 子 mounted -> 父 mounted
* 子组件更新过程
    * 父 beforeUpdate -> 子 beforeUpdate -> 子 updated -> 父 update
* 父组件更新过程
    * 父 beforeUpdate -> 父 updated
* 销毁过程
    * 父 beforeDestroy -> 子 beforeDestroy -> 子 destroyed -> 父 destroyed
#### 在哪个生命周期内调用异步请求
> 一般来说，created、mounted中都可以请求，但大部分会在created中发送请求.
* 在created中调用异步请求有两个优点
    * 能更快获取到服务端的数据，减少页面的loading时间
    * 放在create中有助于一致性，因为ssr不支持 beforeMount 和 mounted 函数
#### 在什么阶段才能访问操作DOM？
> 在mounted中可以访问dom  
> mounted函数被调用前，Vue已经将编译好的模板挂载到页面上

#### 父组件可以监听到子组件的生命周期吗
* 手动$emit触发父组件的事件
```vue
<template>
<div>
    <!--parent-->
    <Child @mounted="doSomething"></Child>
</div>
</template>

<script >
// Child.vue
export default({
    mounted(){
        this.$emit("mounted")
    }
})
   
</script>
```
* 通过@hook
> 不仅可以监听mounted，其他的生命周期都可以监听
```text
//  Parent.vue
<Child @hook:mounted="doSomething" ></Child>

doSomething() {
   console.log('父组件监听到 mounted 钩子函数 ...');
},

//  Child.vue
mounted(){
   console.log('子组件触发 mounted 钩子函数 ...');
},    
// 以上输出顺序为：
// 子组件触发 mounted 钩子函数
// 父组件监听到 mounted 钩子函数
```

### 路由
#### vue-router实现
> 其实是基于HTML5的history API、window.onpopstate、window.onhashchange上做的封装，通过一定的规则映射到对应的方法上，同时监听变化，从而实现单页面路由
#### vue-router 路由模式有几种
> 实际上存在三种
* Hash      使用url的hash值作为路由，支持所有的浏览器
* History   
* Abstract  支持所有js运行模式，如果发现没有浏览器的API，路由会自动强进入这个模式
##### Vue中默认的是hash模式，URL中带有#
可以用代码修改成history模式
```javascript
import Vue from 'vue'
import Router from 'vue-router'
import Main from "@/components/Main"
Vue.use(Router);
export default new Router({
    mode:"history",
    routes:[
        {
            path:"/",
            component:Main
        }
    ]
})
```
#### vue-router 中常用的 hash 和 history 路由模式实现原理

### 组件
#### 谈谈你对 keep-alive 的了解
#### 组件中 data 为什么是一个函数
#### computed 和 watch 的区别和运用的场景
#### v-if和v-show的共同点和区别
#### VUE组件怎么传值/组件之间如何通信
#### Vue 中的 key 有什么作用

### Vuex
> 状态管理工具，所定义的内容，可以在整个Vue的组件内使用，可以理解为一个小型的数据库
#### Vuex成员列表
* state 		存放状态
* getters 		加工state成员给外界
* mutations		state成员操作
* actions 		异步操作
* modules		模块化状态管理

#### 详解成员
* state
	* 以对象的形式存储的数据
	* 使用方式：this.$store.store.name
	* 辅助函数：mapState
* getters
	* 相当于vue组件中的computed；可以借助state的值做一些操作以返回一些新的数据，但无法更改state中的数据
	* 使用方式：this.$store.getters.name
	* 辅助函数：mapGetters
```javascript
import { mapGetters } from 'vuex'
export default {
	computed: {
		// 使用对象展开运算符将 getter 混入 computed 对象中
		...mapGetters([
			'doneTodosCount',
			'anotherGetter',
		])M
		// 重命名
		...mapGetters({
			// 把 `this.doneCount` 映射为 `this.$store.getters.doneTodosCount`
			doneCount: 'doneTodosCount'
		})
	}
}
```
* mutations
	* 相当于vue组件中的methods；可以对state中的数据做操作以达到更改state中的数据
	* 通常情况下使用常量代替utation的事件类型



### 原理性
#### v-model 的原理
#### 怎样理解 Vue 的单向数据流
#### VUE响应式的原理
#### 双向绑定的原理
* [参考1](https://juejin.im/post/5acd0c8a6fb9a028da7cdfaf)
* [参考2](https://juejin.im/post/5acc17cb51882555745a03f8)
#### 怎么实现对象和数组的监听

### 具体操作
#### 直接给一个数组项赋值，Vue 能检测到变化吗
#### VUE中数组如何实现响应式
#### 怎么用 vm.$set() 解决对象新增属性不能响应的问题 

### 优化
#### 对 Vue 项目进行哪些优化

### SSR
#### 说说 Vue SSR
> 服务端渲染，可以优化SEO抓取，提升首页的加载速度

### elementUI怎么做到组件按需加载
### vue3.0特性了解
* 监测机制的改变
* 模板
* 对象式的组件声明方式
* 其它方面的更改

## React
[面试题](https://juejin.im/post/5d5f44dae51d4561df7805b4)
[面试题](https://juejin.im/post/5c989ea76fb9a070ad504cd8)
### React 项目用过什么脚手架
* create-react-app
### 生命周期
[参考](https://zhuanlan.zhihu.com/p/38030418)
#### React生命周期有哪些
* 组件初始化(initialization)阶段
* 组件的挂载(Mounting)阶段
    * componentWillMount
    * render
    * componentDidMount
* 组件的更新(update)阶段
    * componentWillReceiveProps(nextProps)
    * shouldComponentUpdate(nextProps, nextState)
    * componentWillUpdate(nextProps, nextState)
    * render
    * componentDidUpdate(prevProps, prevState)
* 卸载阶段
    * componentWillUnmount
#### react 性能优化是哪个周期函数
> shouldComponentUpdate
#### React最新的生命周期是怎样的
#### React的请求应该放在哪个生命周期中
> componentDidmount
### 组件
#### React 中有三种构建组件的方式
> React.createClass()、ES6 class 和无状态函数。
#### React 中 keys 的作用是什么
#### React的setState是同步还是异步
#### React 中 refs 的作用
#### 组件传值/通信
#### 虚拟DOM实现原理
#### 为什么虚拟DOM会提高性能
#### 展示组件(Presentational component)和容器组件(Container component)之间有何不同
#### 类组件(Class component)和函数式组件(Functional component)之间有何不同
#### (组件的)状态(state)和属性(props)之间有何不同
#### 何为受控组件(controlled component)
#### 何为高阶组件(higher order component)
#### 为什么建议传递给 setState 的参数是一个 callback 而不是一个对象
#### 除了在构造函数中绑定 this，还有其它方式吗
#### (在构造函数中)调用 super(props) 的目的是什么
#### 应该在 React 组件的何处发起 Ajax 请求
#### 描述事件在 React 中的处理方式。
#### createElement 和 cloneElement 有什么区别？
### React Hooks
#### 了解哪些 React Hooks的作用和基本知识
### Redux
#### 优缺点
#### redux的工作流程
#### react-redux是如何工作的
#### redux与mobx的区别
#### redux中如何进行异步操作
#### redux异步中间件之间的优劣
### Redux 和 mobx
### 性能优化
#### React有哪些优化性能是手段
### 算法
#### react diff 原理
#### mixin、hoc、render props、react-hooks的优劣如何
#### 你是如何理解fiber的
#### 你对 Time Slice的理解
# Vue和React的对比/共通点
### Vue和React的区别
#### 相似之处
* 支持组件化
* 数据驱动试图
#### 不同之处  
##### 监听数据变化的实现原理
* Vue : 通过getter/setter和其他函数时间数据劫持
* React 通过比较引用的方式(diff)
##### 数据流不同
* Vue : 双向绑定
* React : 单向数据流
##### 组合不同功能的方式
* Vue mixins
* ReactHoC(高阶组件)
##### 组件通信
> React 本身并不支持自定义事件，而Vue中子组件向父组件传递消息有两种方式：事件和回调函数，但Vue更倾向于使用事件。在React中我们都是使用回调函数的，这可能是他们二者最大的区别
* Vue
    * 父组件通过props向子组件传递数据或者回掉(一般只传数据)
    * 子组件通过事件向父组件发送消息
    * 新增的provide/inject来实现父组件向子组件注入数据，可以跨越多个层级
* React
    * 父组件通过props可以向子组件传递数据或者回调
    * 可以通过 context 进行跨层级的通信
##### 模板渲染方式的不同
* Vue
    * 通过一种拓展的HTML语法进行渲染
    * 在和组件JS代码分离的单独的模板中，通过指令来实现的
* React 
    * React是通过JSX渲染模板
    * React是在组件JS代码中，通过原生JS实现模板中的常见语法，比如插值，条件，循环等，都是通过JS语法实现的
##### 渲染过程不同
* Vue
    * Vue可以更快地计算出Virtual DOM的差异，这是由于它在渲染过程中，会跟踪每一个组件的依赖关系，不需要重新渲染整个组件树
* React
    * 在应用的状态被改变时，全部子组件都会重新渲染。通过shouldComponentUpdate这个生命周期方法可以进行控制，但Vue将此视为默认的优化。
##### 框架本质不同
* Vue
    * Vue本质是MVVM框架，由MVC发展而来
* React 
    * React是前端组件化框架，由后端组件化发展而来
## vue/react框架里如果有错误怎么上报
### Vue
> vue 中 errorCaptured 只能捕获自己子组件的错误，如果子组件出错了，父组件没有处
  理，就会一级一级往上， 如果 app组件还没有处理，根组件也没有处理，就会报错。
  但是不可能在每一个组件里面都使用 errorCaptured 捕获， 而且一个 app 里面可能有
  很多需要错误捕获的地方， 所以建议在 app.vue 中 或者 根组件里面处理
#### 处理方式
* 显示错误页面(配置一个错误路由)
* 收集错误(错误信息，账号信息，手机设备信息等)，提交给后台
``` vue.js
    errorCaptured(error) {
        console.log('root 出错了');
        console.log(error.message);
        // 我们最多只能拿到这个, 如果是在控制台就可以用这样
        // 手机上可以用 android，ios会更清晰
        console.log(window.navigator.userAgent); 
        return false; // 这样就不会在控制台打印了
    }
```
### React
> 只会在最外层处理 react 中的错误
  react 中 index.js 中 render 是处理不了错误的，需要在 App.js 中处理
#### 处理方式
1. getDerivedStateFromError（静态方法）
```react.js
static getDerivedStateFromError(error) { 
    // 1.显示错误提示界面
    // 2.收集错误信息，提交给后台
    return {
        isError: true;
    }
	// 这个 return 的值也会跟 state 进行合并
}
```
2. componentDidCatch（实例方法）
```react.js
componentDidCatch(error) {
    // 1.显示错误提示界面
    // 2.收集错误信息，提交给后台
    this.setState({
        isError: true
    })
}
```
# 性能优化
## 前端性能优化怎么做
## 首屏优化的方法

# 浏览器
## Web生命周期
[参考](https://juejin.im/post/5e9e4c0de51d4546fa453b38)
## 浏览器缓存机制
[参考](https://segmentfault.com/a/1190000008377508)
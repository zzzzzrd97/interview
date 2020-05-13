# CSS+HTML
## HTML
### 关于link
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
#### 响应式中单位的选择及其换算
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

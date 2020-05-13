# JS
## 数据类型
## var let const之间的区别
## 声明提升类问题
### 参考变量对象的创建过程
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
## async await
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

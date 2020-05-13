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
### 常见的状态码

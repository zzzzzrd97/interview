# Vue SSR  [参考](https://segmentfault.com/a/1190000019618170)
## what?
> Server-Side Reading 服务端渲染  
> 所谓服务端渲染，指的是Vue在服务器渲染为组装好的html字符串，然后将他们直接发送到浏览器，最后需要将这些静态标记混合到客户端上完全可交互的应用程序 
## why 为什么选择
* 满足SEO要求，传统的SPA都是异步加载的，爬虫引擎无法加载，需要利用SSR将数据直接渲染在页面源代码中
* 首屏加载更快：在请求页面的时候，服务端直接渲染完数据后返回给浏览器，浏览器只需要解析HTML，不需要再解析js及其他数据、逻辑
## how 如何工作
<img src="https://image-static.segmentfault.com/429/628/429628499-5d17078bcd9ca_articlex">

## 如何搭建

### 初始化一个项目 npm init
### 安装依赖
    npm install express
    npm install vue
    npm install vue-router
    npm install vue-server-renderer  
    
    express 是node端的框架  
    vue 创建vue实例  
    vue-router 实现路由控制  
    vue-server-renderer 实现ssr依赖此库的api
### 创建js
```javascript
const express = require("express");
const app = express();
const Vue = require("vue");
const vueServerRender = require("vue-server-renderer").createRenderer();

app.get('*', (request, response) => {
    const vueApp = new Vue({
        data:{
            message: "hello, ssr"
        },
        template: `<h1>{{message}}</h1>`
    });

    response.status(200);
    response.setHeader("Content-type", "text/html;charset-utf-8");
    vueServerRender.renderToString(vueApp).then((html) => {
        response.end(html);
    }).catch(err => console.log(err))
});

app.listen(3001, () => {
    console.log('服务已开启')
});
```
> vue-server-renderer中的createRenderer对象，有一个renderToString的方法，可以将vue实例转成html的形式。（renderToString这个方法接受的第一个参数是vue的实例，第二个参数是一个回调函数，如果不想使用回调函数的话，这个方法也返回了一个Promise对象，当方法执行成功之后，会在then函数里面返回html结构。）  
> data-server-rendered="true" 表明是由vue-ssr渲染  
> 此时输入localhost:3001 模板已经被渲染出来  

### 将vue实例挂进html中
```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Title</title>
    </head>
    <body>
    <!--vue-ssr-outlet-->
    
    </body>
    </html>
```
> 注意:<!--vue-ssr-outlet-->不能去掉，这是Vue挂载的占位符   

    然后修改server.js，将html模板引进去。这里我们在createRenderer函数可以接收一个对象作为配置参数。配置参数中有一项为template,这项配置的就是我们即将使用的Html模板。这个接收的不是一个单纯的路径，我们需要使用fs模块将html模板读取出来。
```javascript
    let path = require("path");
    const vueServerRender = require("vue-server-renderer").createRenderer({
        template:require("fs").readFileSync(path.join(__dirname,"./index.html"),"utf-8")
    });
```
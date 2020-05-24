> 基于promise的HTTP库
# 安装
## npm安装
> [npm](https://www.npmjs.com/package/axios)   

npm install axios --save
## 引用axios
```html
<script src=https://unpkg.com/axios/dist/axios.min.js"></script>
```
## ES6 import引用
因为axios不是vue的插件，所以不能直接用use方法，需要将其加载到原型上。
```javascript
import axios from 'javascript/axios'
axios.get();
```
如果要全局使用axios就需要在main.js中设置成全局的，然后再组件中通过this调用
```javascript
Vue.prototype.$axios = axios;
this.$axios.get();
```

## 使用
### 基本使用
> get请求
```javascript
// params 查询参数
axios.get('url',{params}).then(res=>{}).catch(err=>{})
```
> post请求
```javascript
axios.post('url',{params}).then(res=>{}).catch(err=>{})
```
> 多个请求合并
```javascript
function request1(){
    return axios.get('url')
}
function request2(){
    return axios.get('url')
}
axios.all([request1(),request2()]).then(axios.spread((res1,res2)=>{
    // 当两个请求都完成时出发axios.spread方法
    // res1是request1的返回结果，res2是request2的返回结果
}))
```
### axios的api
```javascript
axios({
    url:'',
    method:'',
    data:{}
}).then().catch()
```
* axios为所有的请求方式提供了别名
    * axios.request(config)
    * axios.get(url, [config])
    * axios.delete(url, [config])
    * axios.head(url, [config])
    * axios.options(url, [config])
    * axios.post(url, [data], [config]) 
    * axios.put(url, [data], [config])
    * axios.patch(url, [data], [config])

### axios的默认配置
1. 可以通过axios.defaults设置全局默认值，在所有请求中都生效。
```javascript
axios.defaults.headers.common["token"] = "";
axios.defaults.headers.post["Content-type"] = "application/json";   
axios.defaults.baseURL = 'https://service.xxx.com'; //设置统一路径前缀
axios.defaults.withCredentials = true;   // 后端要通过Cookie来验证时的配置
```
2. 也可以自定义实例的默认值，以及修改实例的配置
```javascript
// 创建时自定义默认配置，超时设置为全局默认值0秒
let ax = axios.create({
  baseURL: 'http://rap2api.taobao.org',
  params: { name: '小月' }
});
// 修改配置后，超时设置为4秒
ax.defaults.timeout = 4000; 
```
3. 也可以像前面那样，在每个请求中设置相关的配置
```javascript
axios('/app/mock/121145/get', {
  params: {
    name: 'xiaoxiao'
  },
  baseURL: 'http://rap2api.taobao.org'
})
```
## 拦截器
### 请求拦截器
> 可在此设置token
```javascript
instance.interceptors.request.use(
  config => {
      // do something
      /** eg token
          let token = getToken();
          if(token){
              config.headers.token = token
          }
          return config
      */
  },
  error => {
    return Promise.reject(error)
  })
```

### 响应拦截器
> 在被 then 或者 catch 处理之前
```javascript
    axios.interceptors.response.use(
    res => {
        // do something
        /** eg 返回的数据
            let data = res.data;
            if(data.code===200){
                return data
            }       
        */
    },
    error => {
      return Promise.reject(error)
    })
```

### 取消拦截器
1 取消请求的话需要先通过创建一个CancelToken.source工厂函数创建一个标识source  
2 通过配置项制定标识，这样才知道取消的是哪个请求  
3 调用取消方法  
```javascript
    var CancelToken = axios.CancelToken;
    var source = CancelToken.source(); //1
    axios.post('/user/12345', {
      name: 'new name'
    }, {
      cancelToken: source.token //2
    })
    source.cancel('Operation canceled by the user.'); //3
```
> 还有一种写法是直接把cancelToken的构造函数传递给配置项，该构造函数接受一个函数作为参数，在这个函数中指定标识符。  
```javascript
    var CancelToken = axios.CancelToken;
    var cancel;
    axios.get('/app/mock/121145/get', {
      baseURL: 'http://rap2api.taobao.org',
      cancelToken: new CancelToken(function executor(c) {
        cancel = c;
      })
    });
    cancel();
```
## 跨域
> 服务器和服务器之间是没有跨域的(除非设置了禁止跨域的权限问题); 通过代理服务器请求服务器,然后将数据返回到代理服务器中,之后代理服务器将数据再返回给客户端

如果我们要跨域请求数据，在配置文件里设置代理，vue-cli3项目，需要在根目录自己创建一个vue.config.js，在里面写配置。
```javascript
    module.exports = {
        devServer: {
            proxy: {
                '/api': {
                    target: 'https://www.xxx.com', //目标路径，别忘了加http和端口号
                    changeOrigin: true, //是否跨域
                    ws: true,
                    pathRewrite: {
                        '^/api': '' //重写路径
                    }
                }
           }
        }
    };
```
调用接口：
```javascript
    axios.post('/api/test', {name: 'xiao'}); 
```
[参考1](https://www.jianshu.com/p/f959366fadb8)   
[参考2](https://ykloveyxk.github.io/2017/02/25/axios%E5%85%A8%E6%94%BB%E7%95%A5/#more)


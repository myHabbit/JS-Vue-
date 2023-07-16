##  第    4    章：React ajax  

##   4.1.     理解  

  4.1.1.     前置说明  

1. React本身只关注于界面, 并不包含发送ajax请求的代码
2. 前端应用需要通过ajax请求与后台进行交互(json数据)
3. react应用中需要集成第三方ajax库(或自己封装)

  4.1.2.     常用的    ajax    请求库  

1. jQuery: 比较重, 如果需要另外引入不建议使用
2. axios: 轻量级, 建议使用
3. 封装XmlHttpRequest对象的ajax
4. promise风格
5. 可以用在浏览器端和node服务器端

##   4.2. axios  

###   4.2.1.     文档  

https://github.com/axios/axios

###   4.2.2.     相关    API  

GET请求

```js
axios.get('/user?ID=12345') .then(
 function (response) { 
   console.log(response.data);
 })
 .catch(function (error) {
    console.log(error); });
axios.get('/user', 
   {  params:
   {   ID: 12345  }
   }
) .then(
    function (response) {
        console.log(response); }) 
   .catch(function (error) { 
         console.log(error); });
```

 

```js
POST请求

axios.post('/user',
           { firstName: 'Fred',
            lastName: 'Flintstone'}
          ) .then(
    function (response) {
        console.log(response);})
    .catch(function (error) {
    console.log(error);});
```

## 配置代理

# react脚手架配置代理总结



## 方法一

> 在package.json中追加如下配置

```json
"proxy":"http://localhost:5000"
```

说明：

1. 优点：配置简单，前端请求资源时可以不加任何前缀。
2. 缺点：不能配置多个代理。
3. 工作方式：上述方式配置代理，当请求了3000不存在的资源时，那么该请求会转发给5000 （优先匹配前端资源）



## 方法二

1. 第一步：创建代理配置文件

   ```
   在src下创建配置文件：src/setupProxy.js
   ```

2. 编写setupProxy.js配置具体代理规则：

   ```js
   const proxy = require('http-proxy-middleware')
   
   module.exports = function(app) {
     app.use(
       proxy('/api1', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
         target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
         changeOrigin: true, //控制服务器接收到的请求头中host字段的值
         /*
         	changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
         	changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
         	changeOrigin默认值为false，但我们一般将changeOrigin值设为true
         */
         pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
       }),
       proxy('/api2', { 
         target: 'http://localhost:5001',
         changeOrigin: true,
         pathRewrite: {'^/api2': ''}
       })
     )
   }
   ```

说明：

1. 优点：可以配置多个代理，可以灵活的控制请求是否走代理。
2. 缺点：配置繁琐，前端请求资源时必须加前缀。






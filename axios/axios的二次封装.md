### 1.为什么需要二次封装axios？

请求拦截器 响应拦截器  

请求拦截器  可以在发请求之前可以处理一些业务 

响应拦截器 当服务器返回以后 可以处理一些事情

<img src="C:\Users\G1330\AppData\Roaming\Typora\typora-user-images\image-20230604102358263.png" alt="image-20230604102358263" style="zoom:67%;" />

2.在项目当中经常用api文件夹存放axios

*// 配置对象*

  *// 基础路径 发请求的时候 路径当中会出现api*

  baseURL:'/api',

  *// 代表请求超时的时间5s*

  timeout:5000

参考文档  npm文档

### 2.接口统一管理

项目很小 ：完全可以在组件的生命周期函数(mounted)中发送请求

项目很大 ：axios.get('xxx')

<img src="C:\Users\G1330\AppData\Roaming\Typora\typora-user-images\image-20230604102332864.png" alt="image-20230604102332864" style="zoom:67%;" />



### 3.接口跨域

devServer: {

  proxy: {

   '/api': {*//代理标识，一般是每个接口前的相同部分*

​    target: 'https://you.163.com', *// 这里写的是访问接口的域名和端口号*

​    changeOrigin: true, *// 允许跨域请求*

​    pathRewrite: { *// 重写路径，替换请求地址中的指定路径*

​     '^/api': ''

​    }

   },

  }

 }

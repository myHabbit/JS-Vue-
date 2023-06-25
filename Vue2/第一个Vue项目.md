## 创建第一个vue项目

https://www.jb51.net/article/253584.htm

## Vue.js的引用

script src="https://cdn.jsdelivr.net/npm/vue@2.6.14/dist/vue.js"></script>

<!-- 开发环境版本，包含了有帮助的命令行警告 -->

<script src="https://cdn.jsdelivr.net/npm/vue@2/dist/vue.js"></script>

[vue.js](https://uploader.shimo.im/f/276iezq7ldVXeS3I.js?fileGuid=8Nk6eOYR5rSRJPqL)

 

 

## 新建vue项目

vue create 项目名称  !!不可以用中文 

<img src="file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps4.jpg" alt="img" style="zoom:67%;" /> 

打开文件

 cd my_vue

 $ npm run serve

<img src="file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps5.jpg" alt="img" style="zoom:67%;" /> 

 

<script>基本代码 和MVVM

## MVVM

1.M 模型model 对应的是data中的数据

2。V 视图View 模板

3.VM:视图模型(model view) Vue实例对象

<img src="file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps6.jpg" alt="img" style="zoom:50%;" />  

<img src="file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps7.jpg" alt="img" style="zoom:67%;" /> 

***\*初识Vue\****

1.导入vue.js的script脚本文件

2.在页面中声明一个将要被vue所控制的DOM区域

3.创建vm实例对象(vue实例对象)



```javascript
  <div id="app">
	<h1>你好 {{username}}</h1>
  </div>

    <script type="text/javascript">

 

​    // 创建vue实例

​    const vm = new Vue({

​      el:'#app',  //el用于指定当前Vue实例为那个容器服务，值通常为css的id选择器字符串

​      data:{

​        username:'安鑫'

​      },

​      methods:{}

​    })

  </script>
```

<img src="file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps8.jpg" alt="img" style="zoom:67%;" /> 
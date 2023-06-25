#### vuex的概念以及安装

#### 1.vuex是什么

   1.多组件共享数据

  2.专门在Vue中实现集中式状态（数据）管理的一个Vue插件，对vue应用中多个组件的共享状态进行集中式的管理（读/写） 也是一种组件间通信的方式 且适用于任意组件间通信

#### 什么时候使用Vuex

 1.多个组件依赖于同一个状态

 2.来自不同的组件的行为需要变更同一个状态

https://juejin.cn/post/7182484011543969850  具体使用请看

### Vuex核心

> “**每一个 Vuex 应用的核心就是 store（仓库）。“store”基本上就是一个容器，它包含着你的应用中大部分的状态 (state) 。”**

#### 2.安装

#####   方式一（npm）：

npm install vuex@next --save

安装vuex     npm i vuex

vue2中只能安装vuex3版本  npm i vuex@3

vue3中只能安装vuex4版本  npm i vuex@4

2.使用vuex       Vue.use(Vuex)



##### 方式二（yarn）：

yarn add vuex@next --save

  

##### 3.配置

 在src文件目录下 新建store文件夹 里面新建一个index.js

##### 	配置文件：

###### 引入vue

import Vue from 'vue'

###### 引入vuex

 import Vuex from 'vuex'

##### 使用vuex

 Vue.use(Vuex)

##### 配置文件

 export default new Vuex.Store({ 

 state: {   },  

 getters: {  }, 

 mutations: {  }, 

 actions: {  }, 

 modules: {  } })

##### vue中分为 以下五个状态：

**state** 

  所有共享数据统一放到state中存储 和data相似 在state中定义数据 可以在任何组件中使用

state：{

​	name:'张三',

​	age:18

}

###### 调用方式 

1.标签中直接使用

<div>{{$store.state.name}}</div>

2.在vuex中按需引入

 import { mapState } from "vuex"

<img src="C:\Users\G1330\AppData\Roaming\Typora\typora-user-images\image-20230527210811372.png" alt="image-20230527210811372" style="zoom: 67%;" />

<div><div>

**Mutations** 

更改 Vuex 的 store 中的状态的唯一方法是提交 mutation。Vuex 中的 mutation 非常类似于事件：每个 mutation 都有一个字符串的**事件类型 (type)和一个回调函数 (handler)** 。这个回调函数就是我们实际进行状态更改的地方，并且它会接受 state 作为第一个参数：

**其中参数state参数是必须的，也可以自己传递一个参数(num)，代码如下**

![image-20230527211105815](C:\Users\G1330\AppData\Roaming\Typora\typora-user-images\image-20230527211105815.png)

###### 使用方式

**组件中使用**

<button @click="addFn">增加</button>

 <button @click="subFn">减少</button>
**方法一：使用commit触发Mutation操作**

​	$store.commit("函数名字"，value值)

![image-20230527211719065](C:\Users\G1330\AppData\Roaming\Typora\typora-user-images\image-20230527211719065.png)

**方法二：使用辅助函数进行函数 方法同上**（按需进入）

![image-20230527211919963](C:\Users\G1330\AppData\Roaming\Typora\typora-user-images\image-20230527211919963.png)

##### Actions

Actions和Mutations相似，一般情况下**同步**操作使用Mutations，**异步**操作使用Actions

**组件中调用，提醒:mutations 和 actions 都要在组件的methods中使用 ，而state和getters都**
**是在组件中的computed中使用**

![image-20230527212117422](C:\Users\G1330\AppData\Roaming\Typora\typora-user-images\image-20230527212117422.png)

##### 使用方法

  方法一：使用dispath触发Mutation操作

​	$store.dispath('函数名')

![image-20230527212220441](C:\Users\G1330\AppData\Roaming\Typora\typora-user-images\image-20230527212220441.png)

方法二 ：使用辅助函数进行操作，方法同上

![ ](C:\Users\G1330\AppData\Roaming\Typora\typora-user-images\image-20230527212308276.png)

**Getters**

类似于vue中的computed，进行缓存，对于Store中的数据进行加工处理形成新的数据

**Modules**

由于使用单一状态树，应用的所有状态会集中到一个比较大的对象。当应用变得非常复杂时，store 对象就有可能变得相当臃肿。 为了解决以上问题，Vuex 允许我们将 store 分割成**模块**（module）。每个模块拥有自己的 state、mutation、action、getter、甚至是嵌套子模块——从上至下进行同样方式的分割：



#### dispath 和 commit区别

1. **commit 和 dispatch 两个方法都是传值给vuex的mutation改变state**

2. **区别总的来说他们只是存取方式的不同**

   commit: 用来提交当前模块的mutations

   dispatch: 用来提交当前模块的actions(actions可以提交mutations,可以进行异步操作)

   commit 有些做不到的可以用 dispatch 进行提交

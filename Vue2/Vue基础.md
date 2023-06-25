## 差值语法

 <div id="app">

​    <!-- {{}}为插值语法  功能：用于解析标签体内容 -->

```java
    <h2>{{username}}</h2>

  </div>

 

    <script>

​    const vm = new Vue({

​      el:'#app',

​      data:{

​        username:'安鑫'

​      }

​    })
```

## 指令语法

 

    <div id="app">

```javascript
    <!-- v-bind 指令 可以给任何属性动态绑定值 v-bind:可以简写为: -->

​    <!-- v-bind 指令 用于解析标签（包括：标签属性 标签体内容 绑定事件...） -->

​        <a v-bind:href="url">跳转</a>

  </div>

 

    <script>

​    const vm = new Vue({

​      el: '#app',

​      data: {

​        username: '安鑫',

​        url: 'https://baidu.com'

​      }

​    })

  </script>
```

# 数据绑定

## 单向数据绑定v-bind

v-bind:数据只能从data流向页面

```javascript
    <!-- v-bind为单向数据绑定 -->

​    单项数据绑定:<input type="text" v-bind:value="name">]()

  </div>

 

    <script>

​    const vm = new Vue({

​      el: '#app',

​      data: {

​        name: '安鑫1234'

​      },

​      methods: {}

​    })

  </script>
```

## 双向数据绑定v-model

v-model:数据不仅能从data流向页面，还可以从页面流向data

 <div id="app">

 

```javascript
   <!-- v-model 为双向数据指令 -->

​     <!-- 由于v-model 默认收集的就是value值 所以v-model.value可以简写为v-model: -->

​    双向数据绑定:<input type="text" v-model:value="name">

  </div>

 

    <script>

​    const vm = new Vue({

​      el: '#app',

​      data: {

​        name: '安鑫'

​      },

​      methods: {}

​    })

  </script>
```

注意：v-model只能应用于表单类元素（输入类元素）上

因为v-model默认收集的就是value值

# el与data的两种写法

## el的两种写法

  <div id="app">

```javascript
    <h2>你好 {{username}}</h2>

  </div>

 

    <script>

 

​    // el的两种写法

​    const vm = new Vue({

​      // el:'#app',  //第一种写法  

​      data:{

​        username:'Vue'

​      }

​    })

​    console.log(vm)

​    vm.$mount('#app') //第二种写法

  </script>
```

## data的两种写法

<div id="app">

```javascript
    <h2>你好 {{username}}</h2>

  </div>

 

    <script>

 

​      const vm = new Vue({

​      // el:'#app',

​      // // data的第一种写法：对象式

​      // data:{

​      //   username:'安鑫'

​      // }

 

​      el:'#app',

​      // data的第二种写法：函数式

​      data:function(){

​      console.log('===',this)  //此处的this是Vue实例 

​      return{

​        username:'安鑫'

​      }

​      }

​    })

  </script>
```

注意 由vue管理的函数，一定不要写箭头函数，一旦写了箭头函数 this就不再是vue实例了

# 数据代理

## object.defineproperty方法

```javascript
## 

<script>

​    let number = 18

​    let person = {

​      name: '张三',

​      age: '18'

​    }

​    // 给person对象里面添加一个sex属性 值为男

​    Object.defineProperty(person, 'sex', {

​      // value: '男',

​      // enumerable: true, //控制属性是否可以枚举  默认是false

​      // writable: true,   //控制属性是否可以被修改  默认是false

​      // configurable: true  //控制属性是否可以被删除  默认是false

 

​      // 当有人读取person的age属性时，get函数就会被调用 且返回值就是age的值

​      get() {

​        return number

​      },

 

​      // 当有人修改person的age属性时，get函数就会被调用 且会收到修改的具体值

​      set() {

​        console.log('有人修改了person的age值 其值是',value)

​        number = value

 

​      }

​    })

 

​    // console.log(Object.keys(person));

​    console.log(person);

  </script>
```

## vue中的数据代理

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps9.jpg) 

***\*事件对象\****

***\*基本用法\****

    <div id="app">

​    <h2>欢迎来到{{name}}学习</h2>

​    <button v-on:click="showInfo">点我提示信息</button>

​    <!-- 简写形式 -->

​    <button @click="showInfo2(66,$event)">点我提示信息(传参)</button>

  </div>

    <script>

 

​    const vm = new Vue({

​      el: '#app',

​      data: {

​        name: '尚硅谷'

​      },

​      methods: {

​        showInfo(e) {

​          //   console.log(e.target.innerText)

​          // console.log(this)  //此处的this为vm

​          alert('你好')

​        },

  

​        showInfo2(number,e) {

​          console.log(e.target.innerText)

​          // console.log(this)  //此处的this为vm

​          alert('你好2')

​          console.log(number)

​        },

​      }

​    })

  </script>

vue提供了 v-on事件绑定指令 用来辅助程序员为DOM元素绑定监听事件 语法格式如下:

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps10.jpg) 

 

***\*通过v-on绑定的事件\****

 需要在methods节点中进行声明

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps11.jpg) 

***\*v-on指令的简写形式\****

由于v-on指令在开发中使用频率非常的高 因此 vue官方为其提供了简写形式 简写为(英文的@)

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps12.jpg) 

***\*事件对象event\****

在原生的DOM事件绑定中 可以在处理事务的形参处 接收事件对象event，同理，在v-on指令中（简写为@）,所绑定的事件处理函数中，同样可以接收到事件对象event

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps13.jpg) 

 

***\*绑定事件并传参\****

在使用v-on指令绑定事件时，可以使用()进行传参

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps14.jpg) 

 

***\*$event\****

$event是vue提供的特殊变量，用来表示原生的事件参数对象event,$event可以解决事件参数对象event 被覆盖的的问题

 

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps15.jpg) 

***\*vue里的事件修饰符\****

***\*事件修饰符\****

在事件处理函数中调用preventDefault()或 stopPropagation()是非常常见的需求 因此Vue提供了事件修饰符的概念，来辅助程序员更方便的对事件的触发进行控制，常用的5个是事件修饰符如下：

<!-- 

​    Vue中的事件修饰符:

​      1.prevent：阻止默认行为（常用）

​      2.stop：阻止事件冒泡（常用

​      3.once：事件只触发一次（常用）

​      4.capture：使用事件的捕获模式

​      5.self：只有event.target是当前操作的元素时才触发事件

​      5.passive：事件的默认行为立即执行 无需等待事件回调执行完毕

   -->

***\*键盘事件\****

  <!-- 

​    1.Vue中常见的案件别名：

​     回车 =>enter

​     删除=>delete

​     退出=>esc

​     换行=>tab  必须配合keydown使用

​     空格 =>space

​     上=>up

​     下=>down

​     左=>left

​     右=>right

​     系统修饰键（用法特殊）ctrl alt shift meta 

​     配合keyup使用  按下修饰键的时候 在按下其他按键，随后释放其他键 事件才被触发

​     配合keydown使用，正常触发事件

​     

​     Vue.config.keyCode 去指定具体的按键（不推荐）

   -->

    <div id="app">

​    <h2>欢迎来到{{name}}学习</h2>

​    <input type="text" placeholder="按下回车提示输入" @keyup.enter="showInfo">

  </div>

 

    <script>

​    const vm = new Vue({

​      el: '#app',

​      data: {

​        name: '黑马'

​      },

​      methods: {

​        showInfo(e) {

​          console.log(e.target.value)

​        }

​      }

​    })

  </script>

***\*计算属性-姓名案例\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps16.jpg) 

姓名案例：

 <div id="app">

​    姓: <input type="text" v-model:value="firstName"><br><br>

​    名: <input type="text" v-model:value="lastName"><br><br>

​    全名: <span>{{fullName}}</span>

  </div>

    <script>

​    const vm = new Vue({

​      el:'#app',

​      data:{

​        firstName:'张',

​        lastName:'三',

​      },

​      methods:{

​        demo(){

 

​        }

​      },

​      computed:{

​        fullName:{

​          // get有什么作用？ 当有人读取fullName get就会被调用 切返回值就作为fullName的值

​          // get什么时候调用： 1.初次读取fullName时。2.所依赖的数据发生变化时

​          get(){

​            console.log('get被调用了')

​            // console.log(this);  //此处的this是vm

​            return this.firstName+'-'+this.lastName

​          },

​          set(value){

​            // set 什么时候调用： 当fullName被修改时

​            // console.log('set.value')

​            const arr = value.split('-')

​            console.log(arr)

​            this.firstName = arr[0]

​            this.lastName = arr[1],arr[2]

​             

​          }

​        }

​      }

​    })

  </script>

***\*监视属性\****

***\*天气案例\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps17.jpg) 

***\*监视属性\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps18.jpg) 

***\*监视属性完成天气案例\****

  -->

    <div id="app">

​    <h2>今天天气很{{info}}</h2>

​    <button v-on:click="changeWeather">切换天气</button>

  </div>

 

    <script type="text/javascript">

​    const vm = new Vue({

​      el: '#app',

​      data: {

​        isHot: true

​      },

​      // watch 为监视配置

 

​      methods: {

​        changeWeather() {

​          this.isHot = !this.isHot

​        },

​      },

​      computed: {

​        info() {

​          return this.isHot ? '炎热' : '凉爽'

​        }

​      },

​      watch: {

​        isHot: {

​          // immediate  初始化时 让handler调用一下

​          immediate: true,

​          // handler函数什么时候调用？ 当isHot发生变化时

​          handler(newValue,oldValue) {

​            console.log('info被修改了', newValue, oldValue)

​          }

​        }

​      },

​    })

​    vm.$watch('isHot', {

​      immediate: true,

​      // handler函数什么时候调用？ 当isHot发生变化时

​      handler(newValue, oldValue) {

​        console.log('info被修改了', newValue, oldValue)

​      }

​    })

  </script>

***\*深度监视\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps19.jpg) 

***\*深度监视案例\****

    <div id="app">

​    <h2>今天天气很{{info}}</h2>

​    <button v-on:click="changeWeather">切换天气</button>

​    <hr>

​    <h3>a的值是{{numbers.a}}</h3>

​    <button v-on:click="numbers.a++">点我让a+1</button>

​    <hr>

​    <h3>b的值是{{numbers.b}}</h3>

​    <button v-on:click="numbers.b++">点我让b+1</button>

​    <!-- <button v-on:click="numbers={a:666,b:888}">彻底替换掉numbers</button> -->

  </div>

 

    <script type="text/javascript">

​    const vm = new Vue({

​      el: '#app',

​      data: {

​        isHot: true,

​        numbers: {

​          a: 1,

​          b: 1

​        }

​      },

​      // watch 为监视配置

​      methods: {

​        changeWeather() {

​          this.isHot = !this.isHot

​        },

​      },

​      computed: {

​        info() {

​          return this.isHot ? '炎热' : '凉爽'

​        }

​      },

​      watch: {

​        isHot: {

​          // immediate  初始化时 让handler调用一下

​          // immediate: true,

​          // handler函数什么时候调用？ 当isHot发生变化时

​          handler(newValue, oldValue) {

​            console.log('info被修改了', newValue, oldValue)

​          }

​        },

 

​        // 监视多级结构中某个属性的变化

​        // 'numbers.a': {

​        //   handler() {

​        //     console.log('a被改变了')

​        //   }

​        // }

 

​      // 监视多级结构中所有属性的变化

​        numbers:{

​          // 配置deep  开启深度监视

​          deep:true,

​          handler(){

​            console.log('numbers改变了')

​          }

​        }

​      },

 

​    })

  </script>

***\*深度监视的简写形式\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps20.jpg) 

***\*class与style绑定\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps21.jpg) 

代码块

  <div id="app">

​    <!-- 绑定class样式----字符串写法  适用于：样式的类名不确定 需要动态指定   -->

        <div class="basic" v-bind:class="mood" @click="changeMood">{{name}}</div>

​    <br><br>

 

​    <!-- 绑定class样式----数组写法  适用于：要绑定的样式个数不确定 名字也不确定  -->

        <div class="basic" v-bind:class="classArr" @click="changeMood">{{name}}</div>

​    <br><br> 

 

​    <!-- 绑定class样式----d对象写法  适用于：要绑定的样式个数确定 名字也确定  要动态决定用不用  -->

 

        <div class="basic" v-bind:class="classObj" @click="changeMood">{{name}}</div>

​    <br><br>

        <div class="basic" v-bind:class="{atguigu1:true,atguigu2:false}" @click="changeMood">{{name}}</div>

​    <br>

​    <br>

​    <!--  绑定style样式 --数组写法  -->

        <div class="basic" v-bind:style="styleObj">{{name}}</div>

​    <br><br>

        <div class="basic" v-bind:style="[styleObj,styleObj2]">{{name}}</div>

  </div>

 

    <script type="text/javascript">

​    const vm = new Vue({

​      el: '#app',

​      data: {

​        name: '尚硅谷',

​        mood: 'normal',

​        classArr: ['atguigu1', 'atguigu2', 'atguigu3'],

​        classObj: {

​          atguigu1: false,

​          atguigu2: false,

​        },

​        styleObj:{

​          fontSize:'30px',

​          color:'red'

​        },

​        styleObj2:{

​          backgroundColor: 'orange'

​        }

​      },

​      methods: {

​        changeMood() {

​          const arr = ['happy', 'sad', 'normal']

​          let i = Math.floor(Math.random() * 3)

​          this.mood = arr[i]

​        }

​      },

​    })

 

  </script>

***\*条件渲染v-if v-show\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps22.jpg) 

案例模块：

    <div id="app">

​    <h2>当前的n值是{{n}}</h2>

​    <button @click="n++">点我n+1</button>

​    <!-- 使用v-show完成条件渲染 -->

​    <!-- <h2 v-show="false">欢迎来到{{name}}</h2> -->

​    <!-- <h2 v-show="1 === 1">欢迎来到{{name}}</h2> -->

 

​    <!-- v-if做条件渲染  -->

​    <!-- <h2 v-if="false">欢迎来到{{name}}</h2> -->

​    <!-- <h2 v-if="1 === 1">欢迎来到{{name}}</h2> -->

 

​    <!-- <div v-if="n === 1">Angular</div>

        <div v-else-if="n === 2">React</div>

        <div v-else-if="n === 3">Vue</div>

        <div v-else>哈哈</div> -->

 

​    <!-- template 只能配合v-if使用 -->

​    <template v-if=" n === 1">

​      <h2>你好</h2>

​      <h2>尚硅谷</h2>

​      <h2>西安</h2>

​    </template>

 

  </div>

 

    <script type="text/javascript">

​    const vm = new Vue({

​      el: '#app',

​      data: {

​        name: '尚硅谷',

​        n: 0

​      },

​    })

 

  </script>

***\*列表渲染v-for\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps23.jpg) 

 

***\*列表渲染案例模块\****

 

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps24.jpg) 

***\*key原理\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps25.jpg) 

 

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps26.jpg) 

***\*key作用\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps27.jpg) 

***\*列表的过滤\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps28.jpg) 

***\*vue监测数据改变的原理\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps29.jpg) 

***\*Vue监测数据改变的原理代码块\****

 

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps30.jpg) 

***\*收集表单数据\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps31.jpg) 

***\*收集表单数据代码模块\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps32.jpg) 

***\*过滤器\****

filters

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps33.jpg) 

***\*过滤器代码片段\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps34.jpg) 

***\*v-html指令\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps35.jpg) 

***\*v-text指令\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps36.jpg) 

***\*v-text代码模块\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps37.jpg) 

***\*v-cloak指令\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps38.jpg) 

***\*v-once指令\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps39.jpg) 

***\*代码片段\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps40.jpg) 

***\*v-pre指令\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps41.jpg) 

***\*代码模块\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps42.jpg) 

***\*自定义指令\****

代码模块：

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps43.jpg) 

***\*总结\****

![img](file:///C:\Users\G1330\AppData\Local\Temp\ksohtml588\wps44.jpg) 
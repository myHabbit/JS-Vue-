## 1.概述

###   1.1. SPA    的理解  

1. 单页Web应用（single page web application，SPA）。
2. 整个应用只有  一个完整的页面  。
3. 点击页面中的链接  不会刷新  页面，只会做页面的  局部更新。  
4. 数据都需要通过ajax请求获取, 并在前端异步展现。

###   1.2.     路由的理解  

**1.**   什么是路由    ?  

1. 一个路由就是一个映射关系(key:value)
2. key为路径, value可能是function或component

**2.**   路由分类  

1. 后端路由：
2. 理解： value是function, 用来处理客户端提交的请求。
3. 注册路由： router.get(path, function(req, res))
4. 工作过程：当node接收到一个请求时, 根据请求路径找到匹配的路由, 调用路由中的函数来处理请求, 返回响应数据
5. 前端路由：
6. 浏览器端路由，value是component，用于展示页面内容。
7. 注册路由: <Route path="/test" component={Test}>
8. 工作过程：当浏览器的path变为/test时, 当前路由组件就会变为Test组件

### 1.3. react-router    -dom的理解  

1. react的一个插件库。
2. 专门用来实现一个SPA应用。
3. 基于react的项目基本都会用到此库。

官方文档：[Home v6.4.1 | React Routeropen in new window](https://reactrouter.com/en/main)React Router 以三个不同的包发布到 npm 上，它们分别为：

1. 1. react-router: 路由的核心库，提供了很多的：组件、钩子。
   2. ***\*react-router-dom:\**** **包含react-router所有内容，并添加一些专门用于 DOM 的组件，例如 `<BrowserRouter>`等** 。
   3. react-router-native: 包括react-router所有内容，并添加一些专门用于ReactNative的API，例如:`<NativeRouter>`等。

2. 与React Router 5.x 版本相比，改变了什么？

   1. 内置组件的变化：移除`<Switch/>` ，新增 `<Routes/>`等。

   2. 语法的变化：`component={About}` 变为 `element={<About/>}`等。

   3. 新增多个hook：`useParams`、`useNavigate`、`useMatch`等。

   4. **官方明确推荐函数式组件了！！！**

      ......

安装

```bash
npm install react-router-dom@6
```

### 1.4、路由的基本使用
```js
		1.明确好界面中的导航区、展示区
		2.导航区的a标签改为Link标签
					<Link to="/xxxxx">Demo</Link>
		3.展示区写Route标签进行路径的匹配
					<Route path='/xxxx' component={Demo}/>
		4.<App>的最外侧包裹了一个<BrowserRouter>或<HashRouter>
```

## 2.路由组件与一般组件区别
```js
		1.写法不同：
					一般组件：<Demo/>
					路由组件：<Route path="/demo" component={Demo}/>
		2.存放位置不同：
					一般组件：components
					路由组件：pages
		3.接收到的props不同：
					一般组件：写组件标签时传递了什么，就能收到什么
					路由组件：接收到三个固定的属性
										history:
													go: ƒ go(n)
													goBack: ƒ goBack()
													goForward: ƒ goForward()
													push: ƒ push(path, state)
													replace: ƒ replace(path, state)
										location:
													pathname: "/about"
													search: ""
													state: undefined
										match:
														params: {}
														path: "/about"
														url: "/about"
```

## 3.Link

1. 作用: 修改URL，且不发送网络请求（路由链接）。
2. 注意: 外侧需要用`<BrowserRouter>`或`<HashRouter>`包裹。

```jsx
import { Link } from "react-router-dom";

function Test() {
  return (
    <div>
    	<Link to="/路径">按钮</Link>
    </div>
  );
}
```

## 4.NavLink

作用: 与`<Link>`组件类似，且可实现导航的“高亮”效果。

1.NavLink可以实现路由链接的高亮，通过activeClassName指定样式名

```js
   <NavLink activeClassName="atguigu"to="/about">About</NavLink>
   <NavLink activeClassName="atguigu" to="/home">Home</NavLink>
```



```js
// 注意: NavLink默认类名是active，下面是指定自定义的class

//自定义样式
// 这里的isActive是个boolean值，如果你激活了对应路由就会返回true
<NavLink
    to="login"
    className={({ isActive }) => {
        console.log('home', isActive)
        return isActive ? 'list-group-item myActive' : 'list-group-item'
    }}
>login</NavLink>

/*
	默认情况下，当Home的子组件匹配成功，Home的导航也会高亮，
	当NavLink上添加了end属性后，若Home的子组件匹配成功，则Home的导航没有高亮效果。
	可以说没有用
*/
<NavLink to="home" end >home</NavLink>
```

我们可以把这个逻辑抽离出来

```js
function computeClassName({isActive}){
    return isActive?"list-group-item myActive":"list-group-item";
 }

<NavLink className={computeClassName} to="/about">About</NavLink>
<NavLink className={computeClassName} to="/home">Home</NavLink>
```

### 4.1 封装 NavLink

```js
封装：
import React, { Component } from 'react'
import { NavLink } from 'react-router-dom'

export default class MyNavLink extends Component {
    render() {
        return (
            <div>
                {/* <NavLink activeClassName="atguigu" className="list-group-item" to={to}>{title}</NavLink> */}
                <NavLink activeClassName="atguigu" className="list-group-item" {...this.props}></NavLink>

            </div>
        )
    }
}

使用:
              <MyNavLink to="/about">About</MyNavLink>
              <MyNavLink to="/home" >Home</MyNavLink>
```

## Switch

```js
1.通常情况下，path和component是一一对应的关系。
2.Switch可以提高路由匹配效率(单一匹配)。
```

```js
  将路由用switch包裹着      
    这样当匹配到第一个/home时  就不会继续往下去匹配了
				<Switch>
                  <Route path="/about" component={About} />
                  <Route path="/home" component={Home} />
                  <Route path="/home" component={Test} />
                </Switch>
```

## 解决多级路径刷新页面样式丢失的问题
				1.public/index.html 中 引入样式时不写 ./ 写 / （常用）
				2.public/index.html 中 引入样式时不写 ./ 写 %PUBLIC_URL% （常用）
				3.使用HashRouter

## 路由的严格匹配与模糊匹配
				1.默认使用的是模糊匹配（简单记：【输入的路径】必须包含要【匹配的路径】，且顺序要一致）
				2.开启严格匹配：<Route exact={true} path="/about" component={About}/>
				3.严格匹配不要随便开启，需要再开，有些时候开启会导致无法继续匹配二级路由

## Redirect的使用	

**Redirect 重定向**

				1.一般写在所有路由注册的最下方，当所有路由都无法匹配时，跳转到Redirect指定的路由
				2.具体编码：
						<Switch>
							<Route path="/about" component={About}/>
							<Route path="/home" component={Home}/>
							<Redirect to="/about"/>
						</Switch>

## 5.BrowserRouter和HashRouter

在 React Router 中，最外层的 API 通常就是用 BrowserRouter。BrowserRouter 的内部实现是用了 `history` 这个库和 React Context 来实现的，所以当你的用户前进后退时，`history` 这个库会记住用户的历史记录，这样需要跳转时可以直接操作。

**BrowserRouter与HashRouter的区别**
			1.底层原理不一样：
						BrowserRouter使用的是H5的history API，不兼容IE9及以下版本。
						HashRouter使用的是URL的哈希值。
			2.path表现形式不一样
						BrowserRouter的路径中没有#,例如：localhost:3000/demo/test
						HashRouter的路径包含#,例如：localhost:3000/#/demo/test
			3.刷新后对路由state参数的影响
						(1).BrowserRouter没有任何影响，因为state保存在history对象中。
						(2).HashRouter刷新后会导致路由state参数的丢失！！！
			4.备注：HashRouter可以用于解决一些路径错误相关的问题。

BrowserRouter 使用时，通常用来包住其它需要路由的组件，所以通常会需要在你的应用的最外层用它，比如如下

```javascript
import ReactDOM from 'react-dom'
import * as React from 'react'
import { BrowserRouter } from 'react-router-dom'
import App from './App`

ReactDOM.render(
  <BrowserRouter>
    <App />
  </BrowserRouter>
, document.getElementById('app))
<HashRouter>
```

1. 说明：作用与`<BrowserRouter>`一样，但`<HashRouter>`修改的是地址栏的hash值。

2. 备注：6.x版本中`<HashRouter>`、`<BrowserRouter> `的用法与 5.x 相同。

   ​	**两种router区别**

   ```js
   import React from 'react';
   import ReactDOM from 'react-dom/client';
   import App from './App';
   import { BrowserRouter as Router } from 'react-router-dom'
   // import { HashRouter as Router } from 'react-router-dom'
   
   /* 
      HashRouter 会通过url地址中的hash值来对地址进行匹配
      HashRouter 地址栏会出现#  BrowserRouter不会出现#
   
   
      BrowserRouter直接通过URL地址进行组件的跳转
          使用过程中和我们普通的url地址没有区别
   */
   
   /* 
       react router 可以将url地址和组件进行映射
         当用户访问某个地址时，与其对应的组件会自动的挂载
         当我们通过点击link构建的链接进行跳转时候 跳转并没有经过服务器
         但是当我们刷新页面 或通过普通链接进行跳转时 会向服务器发送请求加载数据
           这时的请求并没有经过react router  所以会返回404
   
     解决方案：
         1.使用HashRouter  服务器不会去判断hash值 
         所以使用HashRouter后请求将会 由React Router处理
         2.需要修改服务器的配置，将所有请求都转发到index.html
   
           location / {
               root   html;
               # index  index.html index.htm;
    	          try-files $url /index.html/;
           }
   
   
   
   
     react router使用步骤
       1.引入react-router-dom包
       2.在index.js中引入BrowserRouter组件
       3.将BrowserRouter设置为根组件
   */
   
   const root = ReactDOM.createRoot(document.getElementById('root'));
   root.render(
     <Router>
       <App></App>
     </Router>
   );
   
   
   
   ```

   

## 6.Routes 与 Route

1. v6版本中移出了先前的`<Switch>`，引入了新的替代者：`<Routes>`。
2. `<Routes>` 和 `<Route>`要配合使用，且必须要用`<Routes>`包裹`<Route>`。
3. `<Route>` 相当于一个 if 语句，如果其路径与当前 URL 匹配，则呈现其对应的组件。
4. `<Route caseSensitive>` 属性用于指定：匹配时是否区分大小写（默认为 false）。
5. 当URL发生变化时，`<Routes> `都会查看其所有子` <Route>` 元素以找到最佳匹配并呈现组件 。
6. `<Route>` 也可以嵌套使用，且可配合`useRoutes()`配置 “路由表” ，但需要通过 `<Outlet>` 组件来渲染其子路由。

**Route**

Route 用来定义一个访问路径与 React 组件之间的关系。比如说，如果你希望用户访问 `https://your_site.com/about` 的时候加载 `<About />` 这个 React 页面，那么你就需要用 Route:

```jsx
<Route path="/about" element={<About />} />
```

**Route组件**

```js
import React from 'react'
import { Route } from 'react-router-dom/cjs/react-router-dom.min'
import Home from './components/Home'
import About from './components/About'
import Menu from './components/Menu'
import Student from './components/Student'
export default function App() {

    return (
        <div>
            <Menu></Menu>
            {/* 
                    component 用来指定路由匹配后被挂载的组件
                        component需要直接传递组件的类
                       通过component构建的组件 他会自动创建  并且会自动传递参数
                        match     --  匹配的信息
                           isExact  检查路径是否完全匹配
                           params    请求的参数
                        location  --地址信息
                        history   --历史记录信息 (控制页面的跳转)
                            push()     跳转页面
                            replace()  替换页面
            */}

            <Route exact path="/" component={Home} />
            <Route exact path="/about" component={About} />
            {/* 
                 /student/:id 会匹配到/student/xxx
            */}
            <Route exact path="/student/:id" component={Student} />
        </div>
    )
}

```

**Routes**

Routes 是用来包住路由访问路径(Route)的。它决定用户在浏览器中输入的路径到对应加载什么 React 组件，因此绝大多数情况下，Routes 的唯一作用是用来包住一系列的 `Route`，比如如下

```jsx
import { Routes, Route } from "react-router-dom";

function App() {
  return (
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
    </Routes>
  );
}
```

在这里，Routes 告诉了 React Router 每当用户访问根地址时，加载 `Home` 这个页面，而当用户访问 `/about` 时，就加载 `<About />` 页面。

**完整代码**

```jsx
<Routes>
    /*path属性用于定义路径，element属性用于定义当前路径所对应的组件*/
    <Route path="/login" element={<Login />}></Route>

		/*用于定义嵌套路由，home是一级路由，对应的路径/home*/
    <Route path="home" element={<Home />}>
       /*test1 和 test2 是二级路由,对应的路径是/home/test1 或 /home/test2*/
      <Route path="test1" element={<Test/>}></Route>
      <Route path="test2" element={<Test2/>}></Route>
	</Route>
	
		//Route也可以不写element属性, 这时就是用于展示嵌套的路由 .所对应的路径是/users/xxx
    <Route path="users">
       <Route path="xxx" element={<Demo />} />
    </Route>
</Routes>
```

## push和replace

```js
开启replace  
   不会留下痕迹
 <Link replace to={{ pathname: '/home/message/detail', state: { id: mapObj.id, title: mapObj.title } }}>{mapObj.title}</Link>

开启replace  
   会留下痕迹
 <Link push to={{ pathname: '/home/message/detail', state: { id: mapObj.id, title: mapObj.title } }}>{mapObj.title}</Link>

```

## 编程式路由导航（路由跳转）
```js
				借助this.prosp.history对象上的API对操作路由跳转、前进、后退
						-this.prosp.history.push()  
						-this.prosp.history.replace()
						-this.prosp.history.goBack()   //后退
						-this.prosp.history.goForward()  //前进
						-this.prosp.history.go()

history:
			go: ƒ go(n)
			goBack: ƒ goBack()
			goForward: ƒ goForward()
			push: ƒ push(path, state)
			replace: ƒ replace(path, state)
```

**类式组件**

```js
import React, { Component } from 'react'
import Detail from './Detail'
import { Link, Route } from 'react-router-dom'

export default class Message extends Component {
    state = {
        messageArr: [
            {
                id: '001',
                title: '消息1'
            },
            {
                id: '002',
                title: '消息2'
            },
            {
                id: '003',
                title: '消息3'
            },
        ]
    }

    replaceShow = (id, title) => {
        // replace跳转 携带params参数
        // this.props.history.replace(`/home/message/detail/${id}/${title}`)

        // replace跳转 携带search参数
        // this.props.history.replace(`/home/message/detail/?id=${id}&title=${title}`)

        // replace跳转 携带state参数
        this.props.history.replace(`/home/message/detail`, { id, title })
    }

    pushShow = (id, title) => {
        // push跳转 携带params参数
        // this.props.history.push(`/home/message/detail/${id}/${title}`)


        // replace跳转 携带search参数
        // this.props.history.push(`/home/message/detail/?id=${id}&title=${title}`)


        // replace跳转 携带state参数
        this.props.history.push(`/home/message/detail`, { id, title })
    }

    go = () => {
        this.props.history.go(2)
    }

    back = () => {
        this.props.history.goBack()

    }
    forword = () => {
        this.props.history.goForward()
    }
    render() {
        const { messageArr } = this.state
        return (
            <div>
                <ul>
                    {
                        messageArr.map(mapObj => {
                            return (
                                <li key={mapObj.id}>
                                    {/* 携带params参数 */}
                                    {/* <Link to={`/home/message/detail/${mapObj.id}/${mapObj.title}`}>{mapObj.title}</Link> */}


                                    {/* 携带search参数 */}
                                    {/* <Link to={`/home/message/detail/?id=${mapObj.id}&title=${mapObj.title}`}>{mapObj.title}</Link> */}

                                    {/* 携带state参数 */}
                                    <Link replace to={{ pathname: '/home/message/detail', state: { id: mapObj.id, title: mapObj.title } }}>{mapObj.title}</Link>
                                    &nbsp;
                                    <button onClick={() => { this.pushShow(mapObj.id, mapObj.title) }}>push查看</button>
                                    &nbsp;
                                    <button onClick={() => { this.replaceShow(mapObj.id, mapObj.title) }}>replace查看</button>

                                </li>
                            )

                        })
                    }
                </ul>
                <hr />
                {/* 声明接受params参数 */}
                {/* <Route path="/home/message/detail/:id/:title" component={Detail} ></Route> */}

                {/* search无需声明接收，正常注册路由即可 */}
                {/* <Route path="/home/message/detail" component={Detail} ></Route> */}

                {/* state无需声明接收，正常注册路由即可 */}
                <Route path="/home/message/detail" component={Detail} ></Route>


                <button onClick={this.back}>回退</button>
                <button onClick={this.forword}>前进</button>
                <button onClick={this.go}>前进多位</button>
            </div>
        )
    }
}

```

## withRouter

```js
import React, { Component } from 'react'
import { withRouter } from 'react-router-dom'


class Header extends Component {
    back = () => {
        this.props.history.goBack()
    }

    render() {
        return (
            <div>
                <div className="page-header">
                    <h2>React Router Demo</h2>
                    <button onClick={this.back}>回退</button>
                </div>
            </div>
        )
    }
}

export default withRouter(Header)

// withRouter() 可以加工一般组件 让一般组件具备路由组件所特有的API
// withRouter的返回值是一个新组件
```



## 7.React Router 实操案例

首先我们建起几个页面

```html
<Home />

<About />

<Dashboard />
```

`Home` 用于展示一个简单的导航列表，`About`用于展示关于页，而 `Dashboard` 则需要用户登录以后才可以访问。

```jsx
import './App.css';
import { BrowserRouter, Route, Routes } from "react-router-dom"

function App() {

  return (
         <BrowserRouter>
            <Routes>
              <Route path="/" element={<Home />} />
            </Routes>
         </BrowserRouter>
  )
}


const Home = () => {
  return <div>hello world</div>
}

export default App;
```

这里我们直接在 `App.js` 中加上一个叫 Home 的组件，里面只是单纯地展示 `hello wolrd` 而已。接下来，我们再把另外两个路径写好，加入 About 和 Dashboard 两个组件

```jsx
import './App.css';
import { BrowserRouter, Route, Routes } from "react-router-dom"

function App() {

  return (
  	<BrowserRouter>
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
      <Route path="/dashboard" element={<Dashboard />} />
    </Routes>
  </BrowserRouter>
  )
}


const Home = () => {
  return <div>hello world</div>
}

const About = () => {
  return <div>这里是卡拉云的主页</div>
}

const Dashboard = () => {
  return <div>今日活跃用户: 42</div>
}

export default App;
```

此时，当我们在浏览器中切换到 `/` 或 `/about` 或 `/dashboard` 时，就会显示对应的组件了。注意，在上面每个 `Route` 中，用 `element` 项将组件传下去，同时在 `path` 项中指定路径。在 `Route` 外，用 `Routes` 包裹起整路由列表。

### 7.1 route组件的几种方式

**1.component**

**2.render**

**3.children**

```js
import React from 'react'
import { Route } from 'react-router-dom/cjs/react-router-dom.min'
import Home from './components/Home'
import About from './components/About'
import Menu from './components/Menu'
import Student from './components/Student'
export default function App() {

    return (
        <div>
            <Menu></Menu>
            {/* 
                    component 用来指定路由匹配后被挂载的组件
                        component需要直接传递组件的类
                       通过component构建的组件 他会自动创建  并且会自动传递参数
                        match     --  匹配的信息
                           isExact  检查路径是否完全匹配
                           params    请求的参数
                        location  --地址信息
                        history   --历史记录信息 (控制页面的跳转)
                            push()     跳转页面
                            replace()  替换页面
            */}

1.
            <Route exact path="/" component={Home} />
            <Route exact path="/about" component={About} />
            {/* 
                 /student/:id 会匹配到/student/xxx
            */}
            {/* <Route exact path="/student/:id" component={Student} /> 			*/}


2.
            {/* 
                render 也可以用来指定要挂载的组件
                  render需要一个回调函数作为参数 回调函数返回值最终被挂载
                  render不会自动传递呢三个属性
            */}
            {/* <Route path="/student/:id" render={
                (routeProps)=>{
                    console.log(routeProps);
                    return <Student match={routeProps}/>
                }
            }></Route> */}


3.
            {/* 
                children 也可以指定被挂载的组件
                    两种用法：
                        1.和render类似  传递回调函数
                            当children设置一个回调函数时 该组件无论路径是否匹配都会挂载

            */}

            <Route path="/student/:id" children={<Student />}> </Route>
			<Route path="/student/:id"><Student /> </Route>
        </div>
    )
}

```



### 7.2获取route属性的方式

1.通过props传递

```js
export default function Student(props) {
    console.log(props.match.params);
    const stu = stuData.find(item => {
        return +props.match.match.params.id === item.id
    })
```

2.钩子函数获取

```js
    const match = useRouteMatch()
    const location = useLocation()
    const history = useHistory()
    const params = useParams()

    const stu = stuData.find(item => {
        return +params.id === item.id
    })

    return (
        <div>
            {stu.id}----{stu.name}
        </div>
    )
```



## 8.如何设置默认页路径(如 404 页)

在上文的路由列表 `Routes` 中，我们可以加入一个 `catch all` 的默认页面，比如用来作 404 页面。

我们只要在最后加入 `path` 为 `*` 的一个路径，意为匹配所有路径，即可

```jsx
function App() {
  return <BrowserRouter>
    <Routes>
      <Route path="/" element={<Home />} />
      <Route path="/about" element={<About />} />
      <Route path="/dashboard" element={<Dashboard />} />
      <Route path="*" element={<NotFound />} />
    </Routes>
  </BrowserRouter>
}

// 用来作为 404 页面的组件
const NotFound = () => {
  return <div>你来到了没有知识的荒原</div>
}
```

## Prompt

**当用户在表单中输入完数据时候 如果点击了跳转页面 则要用该标签弹出提示框**

```js
import React from 'react'
import { Prompt } from 'react-router-dom/cjs/react-router-dom.min'
export default function MyForm() {
    return (
        <div>
            <Prompt
            // 是false没有提示 如果是true就会有提示
                when={false}
                message={'将要离开页面! 确认吗'} />
            <h2>这是一个表单</h2>
            <input></input>

        </div>
    )
}

```

## Redirect

重定向 将路由的跳转重新定向

```js
import React from 'react'
import { Redirect } from 'react-router-dom/cjs/react-router-dom.min'

export default function About(props) {
    /* 
      Redirect 用于跳转页面
    */
    return (
        <div>
            <Redirect push to={'/form'}></Redirect>
            <button>点我一下</button>
            <h2>关于我们,其实是师徒四人</h2>
            <ul>
                <li>孙悟空</li>
                <li>猪八戒</li>
                <li>沙和尚</li>
                <li>唐僧</li>
            </ul>

        </div>
    )
}
```

## react-router V6版本

```js
import React from 'react'
import { Route, Routes } from 'react-router-dom'
import Home from './components/Home'
import About from './components/About'
import Menu from './components/Menu'
export default function App() {
    return (
        <div>
            <h1>App</h1>
            <Menu/>
            {/* 
              Routes 是V6中新增加的组件
                    作用和Switch类似 都是用于Route的容器
                    Routes和Route只有一个会被匹配
                    ！！Route外面必须有Routes
                V6里面 Route的component render children  都变了
                    需要通过element指定要挂载的组件
            */}
            <Routes>
                <Route path="/" element={<Home></Home>}></Route>
                <Route path="/about" element={<About></About>}></Route>
            </Routes>


        </div>
    )
}

```

## V6版本的参数和钩子

```js
import React from 'react'
import { useLocation, useMatch, useNavigate, useParams } from 'react-router-dom'
const stuData = [
    {
        id: 1,
        name: '孙悟空'
    },
    {
        id: 2,
        name: '猪八戒'
    },
    {
        id: 3,
        name: '沙和尚'
    },
    {
        id: 4,
        name: '唐僧'
    },
    {
        id: 5,
        name: '白龙马'
    },
]

export default function Student() {
    // 可以使用useParams()来获取参数
    const { id } = useParams()

    const localtion = useLocation()   //获取当前的地址信息

    const match = useMatch('/about')   //用来检查当前url是否匹配某个路由


    // 如果路径匹配 则返回一个对象 不匹配 则返回null
    console.log(localtion);
    console.log(match);

    // useNavigate() 获取一个用于跳转页面的函数
    const nav = useNavigate()
    console.log(nav);



    const stu = stuData.find(item => {
        return item.id === +id
    })

    const clickHandler = () => {
        // nav('/about')   //点击按钮跳转到 关于页面  使用的是push方式 会产生历史记录
        nav('/about',{
            replace:true  //这样就使用replace 不会产生新的记录
        }) 
    }
    return (
        <div>
            <button onClick={clickHandler}>点我一下</button>
            <h2>{stu.id} -- {stu.name} </h2>
        </div>
    )
}

```

## V6版本的嵌套路由

**Outlet**

```js
定义路由
<Routes>
             <Route path="/about" element={<About></About>}>
                <Route path='hello' element={<Hello></Hello>}>					          </Route>
                </Route>
   </Routes>


                                           
import React from 'react'
import Hello from './Hello'
import { Outlet } from 'react-router-dom'

export default function About() {
  return (
    <div>
      <h2>关于我们</h2>
      <ul>
        <li>刘备</li>
        <li>关羽</li>
        <li>张飞</li>
        <li>赵云</li>
      </ul>
      {/* 
        通过子路由 对hello组件进行映射
      */}
      {/* <Hello/> */}


      {/* 
        Outlet表示嵌套路由中的组件
            当嵌套路由中的路径匹配成功了  outlet则表示嵌套路由中的组件
            当嵌套路由中的路由没有匹配成功 Outlet就什么也不是
      */}
      <Outlet></Outlet>
    </div>
  )
}

```



## 9.Navigate

1. 作用：只要`<Navigate>`组件被渲染，就会修改路径，切换视图。
2. `replace`属性用于控制跳转模式（push 或 replace，默认是push）。

> 相当于5版本的Redirect，对于我来说Redirect语义化会更好的

[http://localhost:3000/home时，展示Home组件；open in new window](http://localhost:3000/home时，展示Home组件；)[http://localhost:3000/about时，展示About组件。open in new window](http://localhost:3000/about时，展示About组件。)[http://localhost:3000/时，既不展示Home组件，也不展示About组件。open in new window](http://localhost:3000/时，既不展示Home组件，也不展示About组件。) 现在，我们使用Redirect Navigate组件实现重定向：`<Route path="/" element={<Navigate to="/about"/>}></Route>`。因此，当访问[http://localhost:3000/时，重定向至http://localhost:3000/about，即默认展示About组件。open in new window](http://localhost:3000/时，重定向至http://localhost:3000/about，即默认展示About组件。)

```jsx
import React from 'react'
import About from "./pages/About";
import Home from "./pages/Home";
import {Route,Routes,Navigate} from "react-router-dom";

<Routes>
    <Route path="/about" element={<About/>}></Route>
    <Route path="/home" element={<Home/>}></Route>
    <Route path="/" element={<Navigate to="/about"/>}></Route>
</Routes>
```

跳转模式的使用:

```jsx
import React,{useState} from 'react'
import {Navigate} from 'react-router-dom'

export default function Home() {
	const [sum,setSum] = useState(1)
	return (
		<div>
			<h3>我是Home的内容</h3>
			{/* 根据sum的值决定是否切换视图 */}
			{sum === 1 ? <h4>sum的值为{sum}</h4> : <Navigate to="/about" replace={true}/>}
			<button onClick={()=>setSum(2)}>点我将sum变为2</button>
		</div>
	)
}
```

## 10.使用useRoutes注册路由

### 10.1 使用useRoutes注册路由表-第一次改进

```
useRoutes()
```

- 作用：根据路由表，动态创建`<Routes>`和`<Route>`。

```jsx
import React from 'react'
import {NavLink,Navigate,useRoutes} from "react-router-dom";
import About from "./pages/About";
import Home from "./pages/Home";

export default function App() {
  const element = useRoutes([
    {
      path:"home",
      element:<Home/>
    },
    {
      path:"about",
      element:<About/>
    },
    {
      path:"/",
      element:<Navigate to="/about"/>
    },
  ])
  return (
    <div>
        <NavLink to="/about">About</NavLink>
        <NavLink to="/home">Home</NavLink>
        <div className="content">
        {element}
        </div>
    </div>
  )
}
```

注意点：**`useRoutes([])`**，useRoutes根据路由表生成对应的路由规则。

### 10.2 第二次改进

src文件夹下新建子文件夹：`routes`，`routes`下新建文件：`index.js` 路由表独立成js文件`：src/routes/index.js`

```
routes/index.js
import { Navigate } from "react-router-dom";
import About from "../pages/About";
import Home from "../pages/Home";

const routes = [
    {
        path:"/about",
        element:<About/>
    },
    {
        path:"/home",
        element:<Home/>
    },
    {
        path:"/",
        element:<Navigate to="/about"/>
    }
]

export default routes;
App.js
import React from 'react'
import {NavLink,useRoutes} from "react-router-dom";
import routes from "./routes";

export default function App() {
  const element = useRoutes(routes);
  return (
    <div>
        <NavLink to="/about">About</NavLink>
        <NavLink to="/home">Home</NavLink>
        <div className="content">
        {element}
        </div>
    </div>
  )
}
```

## 11.嵌套路由的实现

路由结构如下：

- /about，About组件
- /home，Home组件
  - /home/news，News组件
  - /home/message，Message组件

> 在pages文件夹下新建文件夹：News，News下新建文件：index.jsx，即News组件； 在pages文件夹下新建文件夹：Message，Message下新建文件：index.jsx，即Message组件。
>
> 路由表文件routes/index.js pages/Home/index.jsx，即Home组件 pages/News/index.jsx，即News组件 pages/Message/index.jsx，即Message组件

![image-20221027122205526](https://i0.hdslb.com/bfs/album/8a6da962aea796cb490cb74582edd7e18dab8a65.png)image-20221027122205526

```
routes/index.js
```

用 **`children`** 来嵌套路由。

```jsx
import { Navigate } from "react-router-dom";
import About from "../pages/About";
import Home from "../pages/Home";
import News from "../pages/News";
import Message from "../pages/Message";

const routes = [
    {
        path:"/about",
        element:<About/>
    },
    {
        path:"/home",
        element:<Home/>,
        children:[
            {
                path:"news",
                element:<News/>
            },
            {
                path:"message",
                element:<Message/>
            },
        ]
    },
    {
        path:"/",
        element:<Navigate to="/about"/>
    }
]

export default routes;
Home/index.js
```

> ```
> <Outlet>
> ```
>
> 作用：当`<Route>`产生嵌套时，渲染其对应的后续子路由。

```jsx
import React from 'react';
import { NavLink,Outlet } from 'react-router-dom';

export default function Home() {
  return (
    <div>
      <h2>Home组件内容</h2>
      <div>
        <ul className="nav nav-tabs">
          <li>
            {/* <NavLink to="/home/news" className="list-group-item">News</NavLink> */}
            {/* <NavLink to="./news" className="list-group-item">News</NavLink> */}
            <NavLink to="news" className="list-group-item">News</NavLink>
          </li>
          <li>
            <NavLink to="/home/message" className="list-group-item">Message</NavLink>
          </li>
        </ul>
        <Outlet/>
      </div>
    </div>
  )
}
```

- 路由链接中的

   

  `to`

   

  属性值，可以是

  - **`to="/home/news"`**，即全路径(推荐这样写，不然直接看不知道是不是子路由)
  - **`to="./news"`**，即相对路径
  - **`to="news"`**

## 12.路由传递参数

### 12.1 传递 params 参数

需求描述：点击“消息1”，显示其id、title和content。

> pages下新建子文件夹：Detail，Detail下新建文件：index.jsx。pages/Detail/index.jsx即Detail组件。
>
> routes/index.js pages/Message/index.jsx，即Message组件 pages/Detail/index.jsx，即Detail组件
>
> ```js
> {*/\* 声明接收params参数 \*/*}
> 
> <Route path="/home/message/detail/:id/:title" component={Detail} ></Route>
> ```
>
> 

![371844431d4c4553a1fbfd9d01fb140a](https://i0.hdslb.com/bfs/album/cd93da0f0a1b8cb3c10a95316774424e8a90c2a3.gif)371844431d4c4553a1fbfd9d01fb140a

```
routes/index.js
import { Navigate } from "react-router-dom";
import About from "../pages/About";
import Home from "../pages/Home";
import News from "../pages/News";
import Message from "../pages/Message";
import Detail from "../pages/Detail";

const routes = [
    {
        path:"/about",
        element:<About/>
    },
    {
        path:"/home",
        element:<Home/>,
        children:[
            {
                path:"news",
                element:<News/>
            },
            {
                path:"message",
                element:<Message/>,
                children:[
                    {
                        path:"detail/:id/:title/:content",
                        element:<Detail/>
                    }
                ]
            },
        ]
    },
    {
        path:"/",
        element:<Navigate to="/about"/>
    }
]

export default routes;
```

`Message/index.jsx`（Message组件）

**函数组件**

```jsx
import React,{useState} from 'react'
import { NavLink,Outlet } from 'react-router-dom'

export default function Message() {
    const [message] = useState([
        {id:"001",title:"消息1",content:"窗前明月光"},
        {id:"002",title:"消息2",content:"疑是地上霜"},
        {id:"003",title:"消息3",content:"举头望明月"},
        {id:"004",title:"消息4",content:"低头思故乡"}
    ])

    return (
        <div>
            <ul>
            {
                message.map(msgObj => {
                    return (
                        <li key={msgObj.id}>
                            <Link to={`/home/message/detail/${msgObj.id}/${msgObj.title}/${msgObj.content}`}>{msgObj.title}</Link>
                        </li>
                    )
                })
            }
            </ul>
            <hr />
            <Outlet/>
        </div>
    )
}
```

**类组件**

```js
import React, { Component } from 'react'

const detailData = [
    { id: '001', content: '你好,中国' },
    { id: '002', content: '你好,尚硅谷' },
    { id: '003', content: '你好,未来的自己' }
]

export default class Detail extends Component {
    render() {
        const MessageObj = this.props.match.params  //获取params传递的参数
        const { id, title } = MessageObj
        let obj = detailData.find(item => {
            return item.id === id
        })
        return (
            <div>
                <ul>
                    <li>id:{id}</li>
                    <li>title:{title}</li>
                    <li>content:{obj.content}</li>
                </ul>
            </div>
        )
    }
}

```

`Detail/index.jsx`（Detail组件）

> ```
> useParams()
> ```
>
> 作用：回当前匹配路由的`params`参数，类似于5.x中的`match.params`。
>
> ```
> useMatch()
> ```
>
> 作用：返回当前匹配信息，对标5.x中的路由组件的`match`属性。

```jsx
import React from 'react'
import { useParams } from 'react-router-dom'
// import { useMatch } from 'react-router-dom'

export default function Detail() {
  const {id,title,content} = useParams();
  // const {params:{id,title,content}}= useMatch("/home/message/detail/:id/:title/:content");

  return (
    <ul>
      <li>消息编号：{id}</li>
      <li>消息标题：{title}</li>
      <li>消息内容：{content}</li>
    </ul>
  )
}
```

![image-20221027221627763](https://i0.hdslb.com/bfs/album/a48329c789ca77c001be90191437f51399cc7ff0.png)image-20221027221627763

获取params参数有两种方式：

1. 使用 **useParams****`const {id,title,content} = useParams();`**
2. 使用 **useMatch****`const {params:{id,title,content}}= useMatch("/home/message/detail/:id/:title/:content");`**

![image-20221027221736759](https://i0.hdslb.com/bfs/album/3d4eb676c19c7cf4962b27e7bfedff9da5afe804.png)image-20221027221736759

### 12.2 传递 search 参数

演示的需求和上面`params`参数一样，所以只修改关键部分

```
routes/index.js
const routes = [
    {
        path:"/home",
        element:<Home/>,
        children:[
            {
                path:"news",
                element:<News/>
            },
            {
                path:"message",
                element:<Message/>,
                children:[
                    {
                        path:"detail",
                        element:<Detail/>
                    }
                ]
            },
        ]
    },
]

export default routes;
```

`Message/index.jsx`（Message组件）

**函数式组件**

```jsx
export default function Message() {
    return (
        <div>
            <ul>
            {
                message.map(msgObj => {
                    return (
                        <li key={msgObj.id}>
                            <Link to={`detail?id=${msgObj.id}&title=${msgObj.title}&content=${msgObj.content}`}>{msgObj.title}</Link>
                        </li>
                    )
                })
            }
            </ul>
            <hr />
            <Outlet/>
        </div>
    )
}
```

**类式组件**

```js
import React, { Component } from 'react'
import qs from 'querystring-es3'

const detailData = [
    { id: '001', content: '你好,中国' },
    { id: '002', content: '你好,尚硅谷' },
    { id: '003', content: '你好,未来的自己' }
]

export default class Detail extends Component {
    render() {
        // 接收search参数
        const { search } = this.props.location
        const obj = qs.parse(search.slice(1))

        let detailObj = detailData.find(item => {
            return item.id === obj.id
        })
        return (
            <div>
                <ul>
                    <li>id:{detailObj.id}</li>
                    <li>title:{obj.title}</li>
                    <li>content:{detailObj.content}</li>
                </ul>
            </div>
        )
    }
}

```

`Detail/index.jsx`（Detail组件）

> ```
> useSearchParams()
> ```
>
> 作用：用于读取和修改当前位置的 URL 中的查询字符串。 返回一个包含两个值的数组，内容分别为：当前的seaech参数、更新search的函数。
>
> ```
> useLocation()
> ```
>
> 作用：获取当前 location 信息，对标5.x中的路由组件的`location`属性。

**使用useSearchParams**

```jsx
import { useSearchParams } from 'react-router-dom'

export default function Detail() {
  const [search,setSearch] = useSearchParams();
  const id = search.get("id");
  const title = search.get("title");
  const content = search.get("content");

  return (
    <ul>
      <li>
        <button onClick={()=>setSearch('id=008&title=哈哈&content=嘻嘻')}>点我更新一下收到的search参数</button>
      </li>
      <li>消息编号：{id}</li>
      <li>消息标题：{title}</li>
      <li>消息内容：{content}</li>
    </ul>
  )
}
```

![image-20221027222023399](https://i0.hdslb.com/bfs/album/a858b197e7ebe8e56f378dd04606f409d4a30eb4.png)image-20221027222023399

点击按钮后

![image-20221027222047406](https://i0.hdslb.com/bfs/album/7cec34a9494d46fcdcfe7cb6e90d80504c34ca85.png)image-20221027222047406

**使用useLocation**

记得下载安装qs：`npm install --save qs`。

> `nodejs`官方说明`querystring`这个模块即将被废弃，推荐我们使用`qs`模块

```jsx
import { useLocation } from 'react-router-dom'
import qs from "qs";

export default function Detail() {
  const {search} = useLocation();
  const {id,title,content} = qs.parse(search.slice(1));

  return (
    <ul>
      <li>消息编号：{id}</li>
      <li>消息标题：{title}</li>
      <li>消息内容：{content}</li>
    </ul>
  )
}
```

获取search参数，有两种写法：

1. 使用useSearchParams
2. 使用useLocation

### 13.3 传递 state 参数

演示的需求和上面``参数一样，所以只修改关键部分

```
routes/index.js
const routes = [
    {
        path:"/home",
        element:<Home/>,
        children:[
            {
                path:"news",
                element:<News/>
            },
            {
                path:"message",
                element:<Message/>,
                children:[
                    {
                        path:"detail",
                        element:<Detail/>
                    }
                ]
            },
        ]
    },
]

export default routes;
```

`Message/index.jsx`（Message组件）

```jsx
import React,{useState} from 'react'
import { NavLink,Outlet } from 'react-router-dom'

export default function Message() {

    return (
        <div>
            <ul>
            {
                message.map(msgObj => {
                    return (
                        <li key={msgObj.id}>
                            <Link to="detail" state={{ id: msgObj.id, title: msgObj.title, content: msgObj.content }} >{msgObj.title}</Link>
                        </li>
                    )
                })
            }
            </ul>
            <hr />
            <Outlet/>
        </div>
    )
}
```

`Detail/index.jsx`（Detail组件）

**函数式组件**

```jsx
import React from 'react'
import { useLocation } from 'react-router-dom'

export default function Detail() {
  const {state:{id,title,content}} = useLocation();

  return (
    <ul>
      <li>消息编号：{id}</li>
      <li>消息标题：{title}</li>
      <li>消息内容：{content}</li>
    </ul>
  )
}
```

**类式组件**

```js
传递：
 
{/* 携带state参数 */}
<Link to={{ pathname: '/home/message/detail',state:{id:mapObj.id,title:mapObj.title} }}>{mapObj.title}</Link>


接收：
import React, { Component } from 'react'
// import qs from 'querystring-es3'

const detailData = [
    { id: '001', content: '你好,中国' },
    { id: '002', content: '你好,尚硅谷' },
    { id: '003', content: '你好,未来的自己' }
]

export default class Detail extends Component {
    render() {

        // 接收state参数

        const { id, title } = this.props.location.state

        let detailObj = detailData.find(item => {
            return item.id === id
        })

        return (
            <div>
                <ul>
                    <li>id:{id}</li>
                    <li>title:{title}</li>
                    <li>content:{detailObj.content}</li>
                </ul>
            </div>
        )
    }
}
```



> **刷新页面后对路由state参数的影响** 在以前版本中，BrowserRouter没有任何影响，因为state保存在history对象中；HashRouter刷新后会导致路由state参数的丢失 但在V6版本中，HashRouter在页面刷新后不会导致路由state参数的丢失
>
> 但是现在网站基本也没看过路径有个`#`，所以我们使用`BrowserRouter`就行了。

## 14.编程式路由导航（参数）

案例还是和`11.路由传递参数`一样，只是换了种方式传参数

### 14.1 编程式导航下，路由传递params参数

```
pages/Message/index.jsx
import React,{useState} from 'react'
import { NavLink,Outlet,useNavigate } from 'react-router-dom'

export default function Message() {
    const [message] = useState([
        {id:"001",title:"消息1",content:"窗前明月光"},
        {id:"002",title:"消息2",content:"疑是地上霜"},
        {id:"003",title:"消息3",content:"举头望明月"},
        {id:"004",title:"消息4",content:"低头思故乡"}
    ])

    const navigate = useNavigate();

    function handleClick(msgObj){
        const {id,title,content} = msgObj
        navigate(`detail/${id}/${title}/${content}`,{replace:false})
    }

    return (
        <div>
            <ul>
            {
                message.map(msgObj => {
                    return (
                        <li key={msgObj.id}>
                            <NavLink to={`detail/${msgObj.id}/${msgObj.title}/${msgObj.content}`} >{msgObj.title}</NavLink>
                            <button onClick={() => handleClick(msgObj)}>查看消息详情</button>
                        </li>
                    )
                })
            }
            </ul>
            <hr />
            <Outlet/>
        </div>
    )
}
```

### 14.2 编程式导航下，路由传递search参数

```
pages/Message/index.jsx
export default function Message() {

    const navigate = useNavigate();

    function handleClick(msgObj){
        const {id,title,content} = msgObj
        navigate(`detail?id=${id}&title=${title}&content=${content}`,{replace:false})
    }

    return (
        <div>
            <ul>
            {
                message.map(msgObj => {
                    return (
                        <li key={msgObj.id}>
                            <NavLink to={`detail?id=${msgObj.id}&title=${msgObj.title}&content=${msgObj.content}`} >{msgObj.title}</NavLink>
                            <button onClick={() => handleClick(msgObj)}>查看消息详情</button>
                        </li>
                    )
                })
            }
            </ul>
            <hr />
            <Outlet/>
        </div>
    )
}
```

### 14.3 编程式导航下，路由传递state参数

```
pages/Message/index.jsx
export default function Message() {

    const navigate = useNavigate();

    function handleClick(msgObj){
        const {id,title,content} = msgObj
        navigate("detail",{
            replace:false,
            state:{
                id,
                title,
                content
            }
        })
    }

    return (
        <div>
            <ul>
            {
                message.map(msgObj => {
                    return (
                        <li key={msgObj.id}>
                            <NavLink to="detail" state={{ id: msgObj.id, title: msgObj.title, content: msgObj.content }} >{msgObj.title}</NavLink>
                            <button onClick={() => handleClick(msgObj)}>查看消息详情</button>
                        </li>
                    )
                })
            }
            </ul>
            <hr />
            <Outlet/>
        </div>
    )
}
```

### 14.4 withRouter的替换者

这是5版本的时候

```javascript
借助this.prosp.history对象上的API对操作路由跳转、前进、后退
        -this.prosp.history.goBack()
        -this.prosp.history.goForward()
        -this.prosp.history.go(1)
```

我们可以利用 `react-router-dom` 对象下的 `withRouter` 函数来对我们导出的 `Header` 组件进行包装，这样我们就能获得一个拥有 `history` 对象的一般组件

withRouter可以加工一般组件(即非路由组件)，让一般组件具备路由组件所持有的API。但v6版本中已废除，可以直接用useNavigate实现。

```jsx
import React from 'react';
import {useNavigate} from 'react-router-dom'

function Header(props) {

    const navigate = new useNavigate()

    const back = ()=>{
        navigate(-1)
    }

    const forward = ()=>{
        navigate(1)
    }

    const go = ()=>{
        navigate(2)
    }
    
    return (
        <div className="page-header">
            <h2>React Router Demo</h2>
            <button onClick={back}>回退</button>
            <button onClick={forward}>前进</button>
            <button onClick={go}>go</button>
        </div>
    );

}

export default Header;
```


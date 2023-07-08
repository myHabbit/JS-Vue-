## Reducx Tookit(RTK)

### RTK简介

上边的案例我们一克在使用Redux核心库来使用Redux，除了Redux核心库外Redux还为我们投供了一种使用Redux的方式--Redux Toolkit。它的名字起的非常直白，Redux工具包，简称RTK。RTK可以帮助我们处理使用Redux过程中的重复性工作，简化Redux中的各种操作。
在React中使用RTK

### 安装RTK

安装，无论是RTK还是Redux，在React中使用时react-redux都是必不可少，所以使用RTK依然需要安装两个包: 

react-redux和@reduxjs/toolkit.

```js
npm
npm install react-redux @reduxjs/toolkit -S

yarn
yarn add react-redux @reduxjs/toolkit
```

### 使用redux

```js
// 使用RTK来构建store
import { configureStore, createSlice } from '@reduxjs/toolkit'

// createSlice() 创建reducer的切片
/* 
  需要一个配置对象作为参数 通过对象不同的属性 来指定配置信息
*/


const stuSlice = createSlice({
    name: 'stu',      // 用来自动生成action中的type属性的
    initialState: {
        name: '孙悟空',
        age: 18,
        gener: '男',
        address: '花果山'
    },   //state的初始值
    reducers: {           //来指定state的各种操作，可以直接在对象中添加方法
        setName(state, action) {
            // 可以通过不同的方法 来指定state的不同操作
            // 两个参数 state  这个state是个代理对象 我们可以直接修改
            // action
            state.name = '猪八戒'
        },
        setAge(state, action) {
            state.age = 30
        }

    }
})


// 切片对象 会自动帮我们生成action
// actions存储的是slice自动生成的action创建器(函数) 调用函数会自动创建action对象
// actions对象的结构  {type:name/函数名，payload:函数的参数}

export const { setName, setAge } = stuSlice.actions


// console.log(setName('哈哈'));
// console.log(setAge(30));


// 创建state  用来创建state对象  需要一个配置对象作为参数
const store = configureStore({
    reducer: {
        student: stuSlice.reducer
    }
})

export default store

```

### 组件内使用

```js
1.需要在index.js 中使用Provider注入
import React from 'react';
import ReactDOM from 'react-dom/client';
import App from './App';
import store from './store/index'
import {Provider} from 'react-redux'

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <Provider store={store} >
    <App></App>
  </Provider>
);


import React from 'react'
import { useDispatch, useSelector } from 'react-redux'
import { setName,setAge } from './store/index'

export default function App() {
  // useSelector()
  /* 
    useSelector()用来加载state中的数据
  */
  const student = useSelector(state => {
    return state.student
  })

  // 通过usedispath()来获取派发器对象
  const dispatch = useDispatch()

  // 获取action的构建器

  const setNameHandler = () => {
    dispatch(setName('沙和尚'))
  }

  const setAgeHandler = ()=>{
    dispatch(setAge(50))
  }

  return (
    <div>
      <p>
        {student.name}--
        {student.age}--
        {student.gender}--
        {student.address}
      </p>
      <button onClick={setNameHandler}>修改name</button>
      <button onClick={setAgeHandler}>修改age</button>
    </div>
  )
}

```



### 拆分RTK

**1.student**

```js
// 使用RTK来构建store
import {  createSlice } from '@reduxjs/toolkit'

// createSlice() 创建reducer的切片
/* 
  需要一个配置对象作为参数 通过对象不同的属性 来指定配置信息
*/


const stuSlice = createSlice({
    name: 'stu',      // 用来自动生成action中的type属性的
    initialState: {
        name: '孙悟空',
        age: 18,
        gender: '男',
        address: '花果山'
    },   //state的初始值
    reducers: {           //来指定state的各种操作，可以直接在对象中添加方法
        setName(state, action) {
            // 可以通过不同的方法 来指定state的不同操作
            // 两个参数 state  这个state是个代理对象 我们可以直接修改
            // action
            state.name = action.payload
        },
        setAge(state, action) {
            state.age = action.payload
        }

    }
})


// 切片对象 会自动帮我们生成action
// actions存储的是slice自动生成的action创建器(函数) 调用函数会自动创建action对象
// actions对象的结构  {type:name/函数名，payload:函数的参数}

export const { setName, setAge } = stuSlice.actions
export const { reducer:stuReducer } = stuSlice
```

**2.school**

```js
// 使用RTK来构建store
import { createSlice } from '@reduxjs/toolkit'

// 创建一个学校的slice

const schoolSlice = createSlice({
    name: 'school',
    initialState: {
        name: '西安欧亚',
        address: '陕西西安'
    },
    reducers: {
        setName(state, action) {
            state.name = action.payload
        },
        setAddress(state, action) {
            state.address = action.payload
        }
    }
})

export const { setName, setAddress } = schoolSlice.actions
export const { reducer: schoolReducer } = schoolSlice


```

**最后引入**

```js
// 使用RTK来构建store
import { configureStore } from '@reduxjs/toolkit'
import { stuReducer } from './stuSlice'
import { schoolReducer } from './SchoolSlice'



// 创建state  用来创建state对象  需要一个配置对象作为参数
const store = configureStore({
    reducer: {
        student: stuReducer,
        school: schoolReducer
    }
})

export default store

```

#### 组件中使用

```js
import React from 'react'
import { useDispatch, useSelector } from 'react-redux'
import { setName, setAge } from './store/stuSlice'
import { setName as setSchoolName, setAddress } from './store/SchoolSlice'

export default function App() {
  // useSelector()
  /* 
    useSelector()用来加载state中的数据
  */
  // const student = useSelector(state => {
  //   return state.student
  // })

  // // 引入学校state
  // const school = useSelector(state => {
  //   return state.school
  // })

  // 可以结构赋值
  const {student,school}  = useSelector(state => {
    return state
  })

  // 通过usedispath()来获取派发器对象
  const dispatch = useDispatch()

  // 获取action的构建器

  const setNameHandler = () => {
    dispatch(setName('沙和尚'))
  }

  const setAgeHandler = () => {
    dispatch(setAge(50))
  }

  return (
    <div>
      <p>
        {student.name}--
        {student.age}--
        {student.gender}--
        {student.address}
      </p>
      <button onClick={setNameHandler}>修改name</button>
      <button onClick={setAgeHandler}>修改age</button>
      <hr></hr>
      <p>
        {school.name}--
        {school.address}
      </p>
      <button onClick={()=>{ dispatch(setSchoolName('兰州文理学院'))}}>修改学校名字</button>
      <button onClick={()=>{ dispatch(setAddress('甘肃兰州'))}}>修改学校地址</button>
    </div>
  )
}

```


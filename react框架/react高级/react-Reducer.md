## Reducer

### Reducer简介

在React的函数组件中，我们可以通过useState()来创建state。这种创建state的方式会给我们返回两个东西state和setState()。state用来读取数据，而setState()用来设置修改数据。但是这种方式也存在着一些不足，因为所有的修改state的方式都必须通过setState()来进行，如果遇到一些复杂度比较高的state时，这种方式似乎就变得不是那么的优雅。
举个例子，之前的《汉堡到家》的练习中，App.js 中有一个state叫做 cartData 用来存储购物车数据。但是这个数据本身是比较复杂的，它包括了多个属性:

```
const [cartData, setCartData] = useState((
     items:[]，
     totalAmount:0,
     totalPrice:0
3)3
```

### Reducer作用

 为了解决复杂state 带来的不便，React 为我们提供了一个新的使用 state 的方式。Reducer 横空出世，reduce单词中文意味减少，而reducer我觉得可以翻译为“**当你的state的过于复杂时，你就可以使用的可以对state进行整合的工具**”。当然这是个玩笑话，个人认为 Reducer 可以翻译为“整合器”，它的作用就是将那些和同一个 state 相关的所有函数都整合到一起，方便在组件中进行调用。
当然工具都有其使用场景，Reducer 也不例外，它只适用于那些比较复杂的 state，对于简单的state 使用 Reducer 只能是徒增烦恼。但是由于初学，我们会先用一个简单的案例来对其进行演示，实际应用我们后边会以 cartData 作为演示
和state 相同 Reducer 也是一个钩子函数，语法如下:

```js
const [state, dispatch] = useReducer(reducer, initialarg, init);
```

它的返回值和useState()类似，第一个参数是 state 用来读取 state 的值，第二个参数同样是一个函数，不同于 setstate() 这个函数我们可以称它是一个“派发器”，通过它可以向 reducer()

### Reducer用法

```js
import React, { useReducer, useState } from 'react'

// 为了避免reducer会重复创建 通常reducer会定义到组件外部
const countReducer = (state, action) => {

    // 可以根据action不同的type执行不同的操作
    // if (action.type == 'Add') {
    //     return state + 1
    // } else if (action.type == 'Sub') {
    //     return state - 1
    // }

    // // 默认返回当前的state 避免传值无效的情况
    // return state

    switch (action.type) {
        case 'Add':
            return state + 1
            break
        case 'Sub':
            return state - 1
            break
        default:
            return state
    }
};

export default function App() {

    // // 创建一个state
    // const [count, setCount] = useState(1)


    // const addHandler = () => {
    //     setCount(prevState => prevState + 1)
    // }

    // const subHandler = () => {
    //     setCount(prevState => prevState - 1)
    // }


    // useReducer(renucer,initialArg,init)
    /* 
       参数：
         reducer：  整合函数
            对于我们当前state的所有操作 都应该在该函数中定义
             该函数的返回值 会成为state的新值
             reducer在执行的时候 会收到两个参数
                  1.当前最新的state
                  2.命名为action 它需要一个对象 在对象中会存储dispatch所发送的指令
         initialArg: state的初始值  作用和state()中的值是一样的
        返回值：
           返回的是个数组
                第一个参数 ： state  用来获取state的值
                第二个参数：  state修改的派发器
                    通过派发器可以发送操作state的命令
                       具体的修改行为将会由另外一个函数(reducer)执行

    */

    const [count, countDispatch] = useReducer(countReducer, 1)

    //     // 可以根据action不同的type执行不同的操作
    //     // if (action.type == 'Add') {
    //     //     return state + 1
    //     // } else if (action.type == 'Sub') {
    //     //     return state - 1
    //     // }

    //     // // 默认返回当前的state 避免传值无效的情况
    //     // return state


    //     switch (action.type) {
    //         case 'Add':
    //             return state + 1
    //             break
    //         case 'Sub':
    //             return state - 1
    //             break
    //         default:
    //             return state
    //     }
    // }, 1)


    const addHandler = () => {
        // 增加count的值
        countDispatch({ type: 'Add' })
    }

    const subHandler = () => {
        // 增加count的值 
        countDispatch({ type: 'Sub' })
    }


    return (
        <div style={{ fontSize: 30, width: 200, height: 200, margin: '100px auto', textAlign: 'center' }}>
            <button onClick={subHandler}>减少</button>
            {count}
            <button onClick={addHandler}>增加</button>
        </div>
    )
}

```


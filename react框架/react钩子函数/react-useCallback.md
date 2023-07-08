## useCallback

```js
import React, { useCallback, useState } from 'react'
import A from './components/A'

export default function App() {
    console.log('App组件渲染了');

    const [count, setCount] = useState(1)


    const [num, setNum] = useState(1)
    /* 
         useCallback 是一个钩子函数 用来创建react中的一个回调函数
         useCallback  创建回调函数不会总在组件重新渲染时重新创建

         useCallback参数： 
                    1.回调函数
                    2.依赖的数组 
                        当依赖数组中的变量发成变化时 回调函数才会重新创建
                         如果不指定依赖数组，回调函数每次都会重新创建
                         一定要将回调函数中使用到的所有变量都设置到赖数组中

    */

    const clickHandler = useCallback(() => {
        setCount(prevState => prevState + num)
        setNum(prevState => num + 1)
    }, [num])


    return (
        <div>
            <h2>组件App --- {count}</h2>
            <button onClick={clickHandler}>增加</button>
            <A onAdd={clickHandler}></A>
        </div>
    )
}

```


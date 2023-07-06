## useEffect

###  useEffect简介

为了解决这个问题React专门为我们提供了钩子函数 useeffect()，Effect的翻译过来就是副作用，专门用来处理那些不能直接写在组件内部的代码。
哪些代码不能直接写在组件内部呢?像是: 获取数据、记录日志、检查登录、设置定时器等。简单来说，就是那些和组件渲染无关，但却有可能对组件产生副作用的代码.
useEffect语法:

```js
useeffect(didupdate):
```

useEffect() 需要一个函数作为参数，你可以这样写:

```js
useeffect(()=>{
    /”将写那些会产生副作用的代码“/
}):
```

useEffect() 中的回调函数会在组件每次渲染完毕之后执行，这也是它和写在函数体中代码的最大的不同，函数体中的代码会在组件渲染前执行，而 useEffect() 中的代码是在组件渲染后才执行，这就避免了代码的执行影响到组件渲染。
通过使用这个Hook，我设置了React组件

## useEffect用法


​      ** **useEffect是一个钩子函数 需要一个函数作为参数**
​        **这个作为参数的函数 将会在组件渲染完毕后执行**

​     **在开发中  可以将那些会产生副作用的代码编写到useEffect的回调函数中**
​      **这样就可以避免这些代码影响到组件的渲染****

```
import React, { useEffect, useState } from 'react'

export default function App() {
    const [count, setCount] = useState(0)

  
    useEffect(() => {
        setCount(1)
    })


    return (
        <div>
            {count}
        </div>
    )
}

```


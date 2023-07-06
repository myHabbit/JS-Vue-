## setState执行流程

**当我们直接在函数体中调用setState时候。就会触发错误以下错误**
       **Too many re-renders**



###  setState()的执行流程 （函数组件）

​          **setCount() --> dispatchSetData()**
​                **-->先去判断 组件当前处于什么阶段**
​            **渲染阶段              非渲染阶段**

**如果处在渲染阶段   去调用setState  不会检查state的值是否相同**

**如果不是渲染阶段    他会检查state的值是否相同**
   **--> 如果值不同，则将组件进行重新渲染**
   **--> 如果值相同，则不对组件进行重新渲染**
       **如果值相同，我们的react会在一些情况下会继续执行当前组件的渲染**
            **但是这个渲染不会触发其子组件的渲染 这次渲染不会产生实际的效果**
             **这种情况通常发生在第一个相同时**

```js
import React, { useState } from 'react'
import BText from './B'

export default function App() {
    const [count, setCount] = useState(0)


    /* 
        1.count初始值为0 
              第一次点击按钮 count变成了1
                  app组件重新渲染了    执行了
              第二次点击按钮  count也是1
                  app组件重新渲染了     执行了
            第三次点击按钮    count还是1
                  app组件重新渲染了     不执行了

    */

    const addCount = () => {
        setCount(1)
    }

    // setCount(0)

    return (
        <div>
            {count}
            <BText></BText>
            <button onClick={addCount}>点我一下</button>
        </div>
    )
}

```


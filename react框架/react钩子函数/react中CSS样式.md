## 内联样式

写在组件中的样式（不太推荐，代码难以维护）

```js
import React, { useState } from 'react'


export default function App() {
  const [redBorder, setRedBorder] = useState(true)

  const pStyle = {
    color: 'red',
    backgroundColor: '#bfa',
    border: redBorder ? '2px solid red' : '2px solid blue'
  }


  const clickHandler = () => {
    setRedBorder(!redBorder)
  }
  return (
    <div>
      <p style={{
          color:'orange',backgroundColor:'red'
      }}>我是一个段落</p>
 
      <p style={pStyle}>我是一个段落</p>
      <button onClick={clickHandler}>点我一下</button>
    </div>
  )
}

```

## 样式表

css写在外部
在组件中引入  import './App.css'
但是容易发生样式覆盖问题

```js
import React, { useState } from 'react'
import './App.css'

export default function App() {
  const [redBorder, setRedBorder] = useState(false)

  const pStyle = {
    color: 'red',
    backgroundColor: '#bfa',
    border: redBorder ? '2px solid red' : '2px solid blue'
  }


  const clickHandler = () => {
    setRedBorder(!redBorder)
  }
  return (
    <div>
      <p style={pStyle}>我是第一个段落</p>
      <p className={`p1 ${redBorder ? '' : 'blueBorde'}`}>我是第二个段落</p>
      <button onClick={clickHandler}>点我一下</button>
    </div>
  )
}
```

## CSS_Module

相当于模块化css

```js
import React from 'react'
import classes from './App.module.css'

export default function App() {
  /* 
     CSS模块使用步骤
        第一步： 创建一个xxx.module.css
        第二步：  在组件中引入css import classes from './App.module.css'
        第三步：通过classes来设置类
         className={classes.p1}
      
    CSS模块可以动态设置 唯一的class
  */

  return (
    <div>
      <p className={classes.p1}>我是第一个段落</p>
      <button>点我一下</button>
    </div>
  )
}

```


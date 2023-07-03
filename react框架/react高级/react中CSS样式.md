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


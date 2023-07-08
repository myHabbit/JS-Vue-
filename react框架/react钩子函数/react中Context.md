## Context

### Context的讲解：

​                 **-组件间共享数据的方式**

在React中组件间的数据通信是通过props进行的，父组件给子组件设置props，子组件给后代组件设置props，props在组件间自上向下 (父传子)的逐层传递数据。但并不是所有的数据都适合这种传递方式，有些数据需要在多个组件中共同使用，如果还通过props一层一层传递，麻烦自不必多说。

Context为我们提供了一种在不同组件间共享数据的方式，它不再拘泥于props刻板的逐层传递，而是在外层组件中统一设置，设置后内层所有的组件都可以访问到Context中所存储的数据。换句话说，context类似于JS中的全局作用域，可以将一些公共数据设置到一个同一个context中，使得所有的组件都可以访问到这些数据

### Context使用方式

####   创建context

```js
import React from 'react'
/* 
    Context相当于一个公共的存储空间
         我们可以将多个组件中都需要访问的数据统一存储到Context中
          这样无需通过props逐层传递 即可使组件访问到数据

    1.通过React.createContext() 创建context  并且导出   export default testContext


*/

const testContext = React.createContext({
    name: '孙悟空',
    age: 19
})



export default testContext
```

####  组件中使用context

##### 第一种

```js

 import React from 'react'
import testContext from '../src/store/testContext'
/* 
   使用方式1：
      1.引入context
      2.使用xxx.Consumer 组件来创建元素
           Consumer 的标签体需要一个回调函数 
            他会将context设置为回调函数的参数 我们通过参数可以访问到
            context存储的数据

*/

export default function a() {
  return (
    // <div>
    //   我是a组件
    // </div>
    <testContext.Consumer>
      {(ctx) => {
        return <div>
          {ctx.name}-{ctx.age}
        </div>
      }}
    </testContext.Consumer>
  )
}

```

##### 第二种

```js
import React, { useContext } from 'react'
import testContext from './store/testContext'
/* 
   使用context方式二：
     1.导入context
     2.使用钩子函数useContext()来获取到context
        useContext() 需要一个Context作为参数
          他可以将Context中的数据获取并作为返回值返回
*/
export default function B() {
    // 使用钩子函数获取context
    const ctx = useContext(testContext)

    return (
        <div>
            {ctx.name} --{ctx.age}
        </div>
    )
}

```



##### 指定数据的生产者

  **<TestContext.Provider>**
      **表示数据的生产者 来使用他指定context得数据**

​      **-通过value 来指定Context中存储的数据，**

​        **这样一来 在该组件的所有的子组件中都可以通过Context来访问他所指定的数据**

​    **当我们通过context访问数据时，他会读取离他最近的Provider的数据**

​       **如果没有provider 则访问context 中的默认数据**

```
import React, { useState } from 'react'
import Meal from './components/meals/Meals'
import TestContext from './store/testContext'


// 模拟食物数据
const MealsData = [
    {
        id: '1',
        title: '汉堡包',
        desc: '百分百纯牛肉配搭爽脆酸瓜洋葱粒与美味番茄酱经典滋味让你无法抵挡！',
        price: 12,
        img: '/img/meals/1.png'
    },
    {
        id: '2',
        title: '双层吉士汉堡',
        desc: '百分百纯牛肉与双层香软芝，加上松软面包及美味酱料，诱惑无人能挡！',
        price: 20,
        img: '/img/meals/2.png'
    },
    {
        id: '3',
        title: '巨无霸',
        desc: '两块百分百纯牛肉，搭配生菜、洋葱等新鲜食材，口感丰富，极致美味！',
        price: 24,
        img: '/img/meals/3.png'
    }, {
        id: '4',
        title: '麦辣鸡腿汉堡',
        desc: '金黄脆辣的外皮，鲜嫩幼滑的鸡腿肉，多重滋味，一次打动您挑剔的味蕾！',
        price: 21,
        img: '/img/meals/4.png'
    }, {
        id: '5',
        title: '板烧鸡腿堡',
        desc: '原块去骨鸡排嫩滑多汁，与翠绿新鲜的生菜和香浓烧鸡酱搭配，口感丰富！',
        price: 22,
        img: '/img/meals/5.png'
    }, {
        id: '6',
        title: '麦香鸡',
        desc: '清脆爽口的生菜，金黄酥脆的鸡肉。营养配搭，好滋味的健康选择！',
        price: 14,
        img: '/img/meals/6.png'
    }, {
        id: '7',
        title: '吉士汉堡包',
        desc: '百分百纯牛肉与香软芝士融为一体配合美味番茄醬丰富口感一咬即刻涌现！',
        price: 12,
        img: '/img/meals/7.png'
    }
];

export default function App() {

    return (
        <TestContext.Provider>
            <div>
                <Meal
                    mealsData={mealsData}
                    onAdd={addMealHandler}
                    onSub={subMealHandler}
                />
            </div>
        </TestContext.Provider>

    )
}

```


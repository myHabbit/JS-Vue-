## Fetch API

```js
import React, { useEffect, useState } from 'react'
import StudentList from './components/StudentList'

const List = [
    {
        id: 1,
        attributes: {
            name: '孙悟空',
            age: 18,
            gender: '男',
            address: '花果山'
        }
    },
    {
        id: 2,
        attributes: {
            name: '猪八戒',
            age: 19,
            gender: '男',
            address: '高老庄'
        }
    },
    {
        id: 3,
        attributes: {
            name: '沙和尚',
            age: 20,
            gender: '男',
            address: '流沙河'
        }
    },
]

export default function App() {

    const [stuData, setStuData] = useState([])

    /* 
      将写死的数据替换为从接口  http://127.0.0.1:3000/students
         中加载的数据


        组件初始化时我们就需要向服务器发送请求来加载数据
    */

    useEffect(() => {
        // 在Effect发请求
        // fetch() 用来向服务器发送请求加载数据 是ajax的升级版
        // 他需要两个参数  1、请求地址  2.请求信息
        fetch('http://127.0.0.1:3000/students')
            .then((res) => {
                return res.json()
            }).then((data) => {
                // 将加载到的数据来设置到state中
                setStuData(data)
            })
            .catch((error) => {
                console.log(error);
            })
    }, [])


    return (
        <div>
            <StudentList stus={stuData}></StudentList>
        </div>
    )
}

```


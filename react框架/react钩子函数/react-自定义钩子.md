## react -自定义钩子

其实就是用来封装react中的钩子函数用的  必须以use开头的函数

```js
/* 
   react中的钩子函数只能在函数组件或者自定义钩子中调用
   当我们需要将react中的钩子函数提取到一个公共区域时
        我们就可以使用自定义钩子


    自定义钩子其实就是一个普通函数 只是他的名字需要使用use开头

*/

export default function usefetch() {
    const [stuData, setStuData] = useState([])


    const [loading, setLoading] = useState(false)


    const [error, setError] = useState(null)

    const fetchData = useCallback(async function () {
        try {
            setLoading(true)
            // 重置错误
            setError(null)
            const res = await fetch('http://127.0.0.1:3001/students')
            // 请求是否加载成功
            if (res.ok) {
                const data = await res.json()
                setStuData(data)
                setLoading(false)
            } else {
                throw new Error('数据加载失败')
            }
        } catch (error) {
            setError(error)
        } finally {
            setLoading(false)
        }

    }, [])

    // 设置返回值
    return {
        loading,
        error,
        fetchData
    }
}
```


## react-fetch

### 1. 文档  

1. https://github.github.io/fetch/
2. https://segmentfault.com/a/1190000003810652

###   2. 特点  

1. fetch: 原生函数，不再使用XmlHttpRequest对象提交ajax请求
2. 老版本浏览器可能不支持

```js
1、        //发送网络请求(使用fetch发送) then链式实现
        fetch(`https://api.github.com/search/users?q=${keyWord}`, {
            method: 'get'
        }).then(
            res => {
                return res.json()
            })
            // .catch(
            // err => {
            //     console.log('联系服务器失败了', err);
            //     return new Promise()
            // })
            .then(res => {
                console.log(res);
            }).catch(err => {           //统一处理错误
                console.log(err);
            })


2.      //发送网络请求(使用fetch发送) async await 实现
        try {
   const response = await 								                      fetch(`https://api.github.com/search/users?q=${keyWord}`, 				{
      	method: 'get'
     })
            const data = await response.json()
        } catch (error) {
            console.log('请求出错', new Error(error));
        }
    }


    //  https://api.github.com/search/users?q=xxxxxx
```


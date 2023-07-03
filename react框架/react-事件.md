## react事件

在react需要通过元素属性来设置
           ==>  和原生不同  在react中事件的属性要用驼峰命名法
           ==>   onclick  ==>  onClick
           ==>    onchange ==>   onChange
           ==>    属性值不能直接执行代码 而是需要一个回调函数
           ==>    onclick='alert(123)'
           ==>    onClick={ ()=>{ alert(123) }  }

```js
function App() {
    const btn2 = (e) => {
        e.preventDefault();   //取消默认行为
        e.stopPropagation();   //取消事件冒泡

        alert('123')
        /* 
           在react 当中 无法通过return  false取消默认行为
           

           用事件对象方式
               react事件中同样会传递事件对象 可以在响应函数中 定义参数来接受事件对象
               react中的事件对象同样不是原生的事件对象  是经过react包装后新的事件对象
               由于对象进行过包装 所以使用过程无需去考虑兼容性问题
        */
    }

    return <div onClick={() => { alert('div') }} style={{ width: 200, height: 200, margin: '100px auto', background: '#ccc' }}>
        我是APP
        <br />

        {/* 
           在react需要通过元素属性来设置
            和原生不同  在react中事件的属性要用驼峰命名法
               onclick  ==>  onClick
               onchange ==>   onChange
            属性值不能直接执行代码 而是需要一个回调函数
               onclick='alert(123)'
               onClick={ ()=>{ alert(123) }  }
        */}
        <button onClick={() => { alert(123) }}>点我一下</button>

        <button onClick={btn2}>点我</button>
        <br />


        <a href="http://baidu.com" onClick={btn2}>超链接</a>
    </div>
}

/* 
  <button onclick="alert(12)">点我</button>

   <button id="btn">点我</button>


   document.getElementById('btn').onclick=()=>{}
   document.getElementById('btn').addEventListener('click',function(){})
    
*/

export default App
```


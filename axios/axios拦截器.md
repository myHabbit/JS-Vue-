#### axios拦截器

##### 1.请求拦截器

就像一道道关卡一样  满足条件放行 如果所有的请求拦截器都ok 那么就可以发送请求

##### 2.响应拦截器

在我们处理结果之前 可以对结果进行预处理(检查) 如果没问题 交给程序员处理 如果有问题在响应拦截器当中处理掉就行了 我们就不需要处理结果
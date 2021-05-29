#### 1.介绍
+ axios可以基于promise用于浏览器
+ axios可以基于node.js用于http客户端

#### 2.特点
+ 支持浏览器和node.js
+ 支持promise
+ 能转换请求和响应数据
+ 能取消请求
+ 自动转换JSON数据
+ 浏览器端支持防止CSRF(跨站请求伪造)

#### 3.安装
+ npm安装: `npm install axios`
+ bower安装: `bower install axios`
+ cdn引入: `<script src="https://unpkg.com/axios/dist/axios.min.js"></script>`

#### 4.例子
+ GET请求
```
axios.get('/user',{
    params:{
        ID:12345
    }
    })
    .then((res)=>{
        console.log(res)
    })
    .catch((err)=>{
        console.log(err)
    })
```
+ post请求
```
axios.post('/user', {
    firstName: 'Fred',
    lastName: 'Flintstone'
  })
  .then(function (response) {
    console.log(response);
  })
  .catch(function (error) {
    console.log(error);
  });
```
+ 同时发起多个请求
```
function getUserAccount(){
    return axios.get('/user/12345')
}
function getUserPermissions(){
    return axios.get('/user/12345/permissions')
}
axios.all([getUserAccount(),getUserPermissions()])
    .then(axios.spread(function (acct, perms){
        
    }))
```
#### 5.请求方法别名
+ axios.request(config)
+ axios.get(url[, config])
+ axios.delete(url[, config])
+ axios.head(url[, config])
+ axios.options(url[, config])
+ axios.post(url[, data[, config]])
+ axios.put(url[, data[, config]])
+ axios.patch(url[, data[, config]])

#### 6.创建一个实例
axios.creat([config])
```
var instance = axios.create({
    baseURL:'https://some-domain.com/api',
    timeout:1000,
    headers:{'X-Custom-Header':'foobar'}
})
```

#### 7.实例的方法
+ axios#request(config)
+ axios#get(url[, config])
+ axios#delete(url[, config])
+ axios#head(url[, config])
+ axios#options(url[, config])
+ axios#post(url[, data[, config]])
+ axios#put(url[, data[, config]])
+ axios#patch(url[, data[, config]])

#### 8.响应组成
```
{
    data:{},  //服务端返回的数据
    status:200,  //服务端返回的状态码
    statusText:'ok',  //服务端返回的状态信息
    headers:{},  //响应头，且都小写
    config:{},  //请求配置
    request:{}  //请求
}
```
#### 9.默认配置
**1.全局修改axios默认配置**
```
axios.defaults.baseURL = 'https://api.example.com';
axios.defaults.headers.common['Authorization'] = AUTH_THKEN;
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';
```

**2.实例默认配置**
```
//创建实例时修改配置
var instance = axios.create({
    baseURL:'http://api.example.com'
})
//实例创建之后修改配置
instance.defaults.headers.common['Authorization'] = AUTH_TOKEN;
```

**3.配置优先级**
request config > instance.defaults > 系统默认

**4.拦截器**
在then和catch之前拦截请求和响应
```
//请求拦截
axios.interceptors.request.use(function(config){
    //do something
    return config;
},function(error){
    //do something
    return Promise.reject(error);
})

//响应拦截
axios.interceptors.response.use(function(response){
    //do something
    return response;
},function(error){
    //do something
    return Promise.reject(error);
})
```
**5.移除拦截器**
```
var myInterceptor = axios.interceptors.request.use(function () {/*...*/});
axios.interceptors.request.eject(myInterceptor);
```
**6.错误处理**
```
axios.get('/user/12345')
  .catch(function (error) {
    if (error.response) {
      // 发送请求后，服务端返回的响应码不是 2xx   
      console.log(error.response.data);
      console.log(error.response.status);
      console.log(error.response.headers);
    } else if (error.request) {
      // 发送请求但是没有响应返回
      console.log(error.request);
    } else {
      // 其他错误
      console.log('Error', error.message);
    }
    console.log(error.config);
  });
```
**7.取消请求**
```
var CancelToken = axios.CancelToken;
var source = CancelToken.source();

axios.get('/user/12345', {
  cancelToken: source.token
}).catch(function(thrown) {
  if (axios.isCancel(thrown)) {
    console.log('Request canceled', thrown.message);
  } else {
    // handle error
  }
});

// cancel the request (the message parameter is optional)
source.cancel('Operation canceled by the user.');
```
******
+ 摘自   
[axios中文文档](https://www.jianshu.com/p/7a9fbcbb1114)
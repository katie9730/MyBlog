## 第四章：react ajax
### 4.1 理解
#### 4.1.1 前置说明
- React本身只关注于界面，并不包含发送ajax请求的代码
- 前端应用需要通过ajax请求与后台进行交互（json数据）
- react应用中需要集成第三方ajax库（或自己封装）

#### 4.1.2 常用的ajax请求库
- jQuery：太重，如果需要另外引用不建议使用
- axios：轻量级，建议使用
    + 封装XmlHttpRequest对象的ajax
    + promise风格
    + 可以用在浏览器端和nodo服务器端

### 4.2 axios
#### 4.2.1 文档
- https://github.com/axios/axios

#### 4.2.2 相关API
- GET请求
```
axios.get('/user?id=12345')
    .then(function(res) {
        console.log(res.data)
    })
    .catch(function(error){
        console.log(error)
    })
```
- POST请求



## 69集 
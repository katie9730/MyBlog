#### 1.介绍
SuperAgent是轻量级渐进式ajax API。使用于NodeJS环境中。  
[官方文档](http://visionmedia.github.io/superagent/#test-documentation) [简书文档](https://www.jianshu.com/p/1432e0f29abd)
使用示例：
```
var request = require('superagent')
request
    .post('/api/pet')
    .send({ name:'Manny', species:'cat' })
    .set('X-API-Key','foobar')
    .set('Accept','application/json')
    .then(res=>{
        alert('yay got' + JSON.stringify(res.body))
    })
```

#### 2.请求基础知识
通过调用request对象，携带请求方法类型（get`默认`，post，put，patch，head，delete），通过.then()方法或.end()方法或await关键字发送请求启动请求。

注意：
+ 在旧版本浏览器中`delete`是系统关键字，为了兼容，可以调用`del`方法来避免冲突。

#### 3.设置头部字段
报文header字段设置通过调用set()方法。
```
// 写法一
request
    .get('/search')
    .set('API-Key','foobar')
    .set('Accept','application/json')
    .then(callback)
 
// 写法二
 request
   .get('/search')
   .set({ 'API-Key': 'foobar', Accept: 'application/json' })
   .then(callback);    
```

#### 4.GET请求
当我们使用GET请求传递查询字符串时，可以使用query()方法，同时传递一个对象作为参数。
+ 当然query可合并成一条，参数拼接使用`&`字符；
+ query也可接受字符串或者一个对象；
```
request
    .get('/search')
    .query({query:'manny'})
    .query({range:'1..5'})
    .query({order:'desc'})
    .then(res=>{
        
    })
//生成路径为/search?query=Manny&range=1..5&order=desc
```

#### 5.Head请求
该方法也接受`.query()`对象，基本于get()类似。

#### 6.post/put请求
+ JSON成为通用的数据格式后，request对象默认`Content-Type`为`application/json`。
+ 然而默认情况下，发送字符串时，`Content-Type`为`application/x-www-form-urlencoded`。
+ 当然SuperAgent请求的数据格式是可以扩展的，比如可以调用`type(form)`
```
// 默认json格式
request.post('/user')
  .send('{"name":"tj","pet":"tobi"}')
  .then(callback)

// form格式
request.post('/user')
    .type('form')
    .set('Content-Type', 'application/json')
    .send('{"name":"tj","pet":"tobi"}')
    .then(callback)
    .catch(errorCallback)
    
// formData对象
request.post('/user')
    .send(new FormData(document.getElementByID('myForm')))
    .then(callback)
```

#### 7.设置Content-Type
使用`.set()`方法
```
request.post('/user')
    .type('application/json')
    
request.post('/user')
    .type('json')

request.post('/user')
    .type('png')
```

#### 8.序列化请求体
SuperAgent自动序列化JSON和表单数据，也可以为其他类型设置自动序列化。
```
request.serialize['application/xml'] = function(obj){
    return 'string generated from obj'
}

// 自定义格式发送数据
request
    .post('/user')
    .send({foo:'bar'})
    .serialize(obj =>{
        return 'string generated from obj'
    })
```

#### 9.重发请求
使用`.retry`方法，SuperAgent将自动重试请求。   
此方法接受两个可选参数：重试次数（默认值为3）和回调。
```
 request
   .get('https://example.com/search')
   .retry(2) // or:
   .retry(2, callback)
   .then(finished);
   .catch(failed);
```

#### 10.设置Accept
与`type()`方法一致，这里可以调用`accept()`方法来设置Accept接受类型，该值会被request.types所引用。
```
request.get('/user')
    .accept('application/json')
    
request.get('/user')
  .accept('json')

request.post('/user')
  .accept('png')
```

#### 11.查询字符串
`req.query(obj)`是一种用于构建查询字符串的方法。默认情况下，查询字符串不按任何特定顺序组合。    
`req.sortQuery`提供自定义排序比较功能。
```
 // default order
 request.get('/user')
   .query('name=Nick')
   .query('search=Manny')
   .sortQuery()
   .then(callback)

 // customized sort function
 request.get('/user')
   .query('name=Nick')
   .query('search=Manny')
   .sortQuery((a, b) => a.length - b.length)
   .then(callback)
```

#### 12.TLS选项
在Node.js中，SuperAgent支持配置HTTPS请求的方法
+ `.ca()`：将CA证书设置为信任
+ `.cert()`：设置客户端证书链
+ `.key()`：设置客户端私钥
+ `.pfx()`：设置客户端PFX或PKCS12编码的私钥和证书链

```
var key = fs.readFileSync('key.pem'),
    cert = fs.readFileSync('cert.pem');

request
  .post('/client-auth')
  .key(key)
  .cert(cert)
  .then(callback);var key = fs.readFileSync('key.pem'),
    cert = fs.readFileSync('cert.pem');

request
  .post('/client-auth')
  .key(key)
  .cert(cert)
  .then(callback);
```

#### 13.解析响应体
SuperAgent 可以解析常用的响应体，目前支持application/x-www-form-urlencoded，application/json， 和multipart/form-data格式。
```
// 浏览器端使用SuperAgent
request.parse['application/xml'] = function (str) {
    return {'object': 'parsed from str'};
};

// Node中使用SuperAgent
request.parse['application/xml'] = function (res, cb) {

    // 解析响应内容，设置响应体代码

    cb(null, res);
};

// 自动解析响应体
```

## 未完待续 2019/9/18
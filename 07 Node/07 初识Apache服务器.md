#### 1.127.0.0.1\、localhost和本地IP地址三者的区别
+ localhost等于127.0.0.1，不过localhost为域名，127.0.0.1为IP地址。两者都无需联网，都是本地访问。
+ 本地IP需要联网，本机IP是本机或外部访问，本机IP就是本机对外开放访问的IP地址，这个网址就是物理网卡绑定的IP地址。

#### 2.创建简单的web服务
```
var http = require('http')

//1.创建 server
var server = http.createServer()

//2.监听server的request请求事件，设置请求处理函数
//请求->处理
//响应->一个请求对应一个响应，如果在一个请求的过程中，已经结束了响应，则不能重复发送响应，因为没有请求就没有响应。
server.on('request', function (req, res){
    var url = req.url
    if (url === '/'){
        res.end('hello world')
    }else{
        res.end('404 Not Found.')
    }
})

//3.绑定端口号，启动服务
server.listen(3000, function (){
    console.log('running...')
})

```


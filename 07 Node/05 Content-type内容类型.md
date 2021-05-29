```
var http = require('http')

var server = http.createServer()

server.on('request',function(req, res){
    // 在服务端默认发送的数据，其实是 utf8 编码的内容
    // 但是浏览器不知道你是 utf8 编码内容
    // 浏览器在不知道服务器响应内容的编码的情况下会按照当前操作系统的默认编码去解析
    // 中文操作系统默认是 GBK
    // 解决方法就是正确的告诉浏览器我给你发送的内容是什么编码的
    // 在http协议中
    // res.setHeader('Content-Type','text/plain; charset=utf-8')
    // res.end('hello 世界')

    var url = req.url
    if (url === '/plain'){
        //text-plain 就是普通文本
        res.setHeader('Content-Type','text/plain; charset=utf-8')
        res.end('hello 世界')

        //如果你发送的是 html 格式的字符串，则也要告诉浏览器我给你发送的时 text/html 格式的内容
        res.setHeader('Content-Type','text/html; charset=utf-8')
        res.end('<p>hello html <a href="/">点我</a></p>')
    }

})

server.listen(3000, function(){
    console.log('server is running')
})

```

```
var http = require('http')
var fs = require('fs')

var server = http.createServer()

server.on('request',function(req,res){
    //我们要发送的还是在文件中的内容
    fs.readFile('./resource/index.html',function(err, data){
        if(err){
            res.setHeader('Content-Type','text/html; charset=utf-8')
            res.end('文件读取失败，请稍后重试！')
        }else{
            // data 默认是二进制数据，可以通过 .toString 转为咱们能识别的字符串
            // res.end() 支持两种数据类型，一种是二进制，一种是字符串
            res.setHeader('Content-Type','text/html; charset=utf-8')
            res.end(data)

            //url:统一资源定位器
            //一个url 最终其实是要对应一个资源的
            //图片不需要指定编码，因为我们常说的编码一般指的是：字符编码  `image/jpeg`
        }
    })
})

server.listen(3000, function(){
    console.log('server is running…')
})

```

- 1.结合 fs 发送文件中的数据
- 2.Content-Type类型对照表:      + http://tool.oschina.net/commons
  + 不同的资源对应的Content-Type是不一样的
  + 图片不需要指定编码
  + 一般只为字符数据才指定编码
- 3.除了Content-Type可以用来指定编码，也可以在HTML页面中通过源数据来声明文本的编码格式，浏览器会去识别它。
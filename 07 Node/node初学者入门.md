#### 1.应用不同模块分析
+ 我们需要提供Web页面，因此需要一个HTTP服务器
+ 对于不同的请求，根据请求的URL，我们的服务器需要给予不同的响应，因此我们需要一个路由，用于把请求对应到请求处理程序（request handler）
+ 当请求被服务器接收并通过路由传递之后，需要可以对其进行处理，因此我们需要最终的请求处理程序
+ 路由还应该能处理POST数据，并且把数据封装成更友好的格式传递给请求处理入程序，因此需要请求数据处理功能
+ 我们不仅仅要处理URL对应的请求，还要把内容显示出来，这意味着我们需要一些视图逻辑供请求处理程序使用，以便将内容发送给用户的浏览器
+ 最后，用户需要上传图片，所以我们需要上传处理功能来处理这方面的细节

#### 2.构建应用模块
**2.1 创建一个基础的HTTP服务器**
```
// 请求（require）Node.js自带的 http 模块，并且把它赋值给 http 变量。
var http = require("http");

// 调用http模块提供的函数(createServer)创建服务器
// 使用listen方法，指定HTTP服务器监听端口号
http.createServer(function(request, response){
  response.writeHead(200,{"Content-Type":"text/plain"});
  response.write("Hello World");
  response.end();
}).listen(8888);

// 启动服务
node server.js
```
**2.2 进行函数传递**
```
function say(word){
    console.log(word)
}

function execute(someFunction, value){
    someFunction(value);
}

execute(say,'Hello');
```
say变成了execute中的本地变量someFunction，execute可以通过调用someFunction()来使用say函数。
> 总结     
在JavaScript中，一个函数可以接受另一个函数作为参数。可以先定义在传递，也可以传递参数的地方直接定义函数。

**2.3 函数传递是如何让HTTP服务器工作的**
```
var http = require('http')

function onRequest(request,response){
    response.writeHead(200,{'Content-Type':'text/plain'});
    response.write('Hello World!');
    response.end();
}

http.createServer(onRequest).listen(8888);
```
**2.4 基于事件驱动的回调**
Node.js是基于事件驱动的。
```
var http = require('http')

function onRequest(request,response){
    console.log('Request received');
    response.writeHead(200,{'content-Type':'text/plain'})
    response.write('Hello World');
    response.end();
}

http.createServer(onRequest).listen(8888);
console.log('Server has started.')

//运行node server.js时，会马上在命令行输出'Server has started'。当我们向服务器发出请求（在浏览器访问http://localhost:8888/）,'Request received'这条消息就会在命令行出现。
```
**2.5 服务器是如何处理请求的**
onRequest()部分即回调函数。   
+ 第一步：当回调启动，我们的onRequest()函数被触发的时候，request和response两个参数对象被传入；
+ 第二步：服务器收到请求后，使用response.writeHead()函数发送一个HTTP状态200和HTTP头的内容类型(content-type)+ + 第三步：使用response.write()函数在HTTP相应主体中发送文本"Hello World"
+ 第四步：最后调用response.end()完成响应。

**2.6 服务端的模块放在哪里**
将服务器脚本放到start函数里，然后到处这个函数
```
[server.js]
var http = require('http')

function start(){
    function onRequest((request, response){
        console.log('Request received');
        response.writeHead(200, {'Content-Type':'text/plain'});
        response.wirte('Hello World');
        response.end();
    })
    
    http.createSerer(onRequest).listen(8888);
    console.log('Server has started.')
}

exports.start = start;

[index.js]
var server = require('./server');
server.start();
```
这样子就可以像使用任何其他的内置模块一样使用server模块了。请求这个文件，并把它指向一个变量。其中已经用export导出的函数就可以被使用了。
**2.7 如何来进行请求的“路由”**   
我们需要的所有数据都包含在request对象中，包含提供请求的URL和需要的GET及POST参数，然后根据这些数据来执行相应的代码 。然后需要Node.js模块（url和querystring）来解析这些数据。
+ 使用querystring模块解析post请求体中的参数
```
[server.js]
var http = require('http')
var url = require('url')

function start(route){
    function onRequest(request, response){
        var pathname = url.parse(request.url).pathname;
        console.log('Request for ' + pathname + 'received.');
        
        route(pathname);
        
        response.writeHead(200,{'Content-Type':'text/plain'});
        response.write('Hello World')
        response.end();
    }
    http.createServer(onRequest).listen(8888);
    console.log('Server has started');
}
exports.start = start

[index.js]
var server = require('./server');
var router = require('./router');
server.start(router.route)

[router.js]
function route(pathname){
    console.log('About to route a request for ' + pathname);
}
exports.route = route;
```
**2.8 路由给真正的请求处理程序**
是指我们要针对不同的URL有不同的处理方式。把作为路由目标的函数称为请求处理程序。对于每一个请求处理程序，添加一个函数用以占位，随后将这些函数作为模块的方法导出。
```
function start(){
    console.log("equest handler 'start' was called.");
}

function upload(){
    console.log("Request handler 'upload' was called.");
}

export.start = start;
export.upload = upload;

```
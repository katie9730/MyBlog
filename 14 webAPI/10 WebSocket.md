#### 1.简介
首先WebSocket是一种网络通信协议。是服务器推送技术的一种。
**HTTP与WebSocket的区别**
+ HTTP协议：通信只可由客户端发起，为单向请求。
+ WebSocket协议：通信可由客户端->服务器、服务端->客户端发起，为双向请求。
    - 建立在TCP协议之上，服务器端实现较容易。
    - 与HTPP有良好的兼容性。默认端口为80和443。握手采用HTTP协议。
    - 数据格式轻量，性能开销小，通信效率高。
    - 可发送文本，也可二进制数据。
    - 没有同源限制，客户端可与任意服务器通信，取代Ajax。
    - 协议标识符为ws（若加密则是wss，对应HTTPS协议），服务器网址为URL。

#### 2.WebSocket握手
```
// 浏览器发出
GET / HTTP/1.1
Connection: Upgrade  //浏览器通知服务器，若可以则升级到websocket协议
Upgrade: websocket  //HTTP头。该字段指定的协议。
Host: example.com
Origin: null  //用于提供请求发出的域名，供服务器验证。
Sec-WebSocket-Key: sN9cRrP/n9NdMgdcy2VJFQ==  //用于握手协议的密钥，Base64编码的16字节随机字符串
Sec-WebSocket-Version: 13

//服务器回应
HTTP/1.1 101 Switching Protocols
Connection: Upgrade  //通知浏览器，需要改变的协议
Upgrade: websocket
Sec-WebSocket-Accept: fFBooB7FAkLlXgRSz0BT3v4hq5s=  //浏览器对这个值验证，以证明确实是目标服务器回应了WebSocket请求
Sec-WebSocket-Origin: null
Sec-WebSocket-Location: ws://example.com/  //表示进行通信的WebSocket网址
```
完成握手之后，WebSocket就在TCP协议上，开始传送数据。

#### 3.客户端的简单示例
```
var ws = new WebSocket('wss://echo.websocket.org');

ws.onopen = function(evt){
  console.log('Connection open ...');
  ws.send('Hello WebSockets!');
}

wx.onmessage = function(evt){
    console.log('Received Message: ' + evt.data);
    ws.close();
}

ws.onclose = function(evt){
      console.log('Connection closed.');
}
```

#### 4.客户端API
浏览器对WebSocket协议的处理
+ 建立连接和断开连接
+ 发送数据和接数据
+ 处理错误

**4.1 构造函数 WebSocket**
```
//新建WebSocket实例
var ws = new WebSocket('ws://localhost:8080')
//客户端与服务器进行了连接
```

**4.2 webSocket.readyState**
返回实例对象的当前状态
+ CONNECTING：值为0，表示正在连接
+ OPEN：值为1，表示连接成功，可以通信
+ CLOSING：值为2，表示连接关闭
+ CLOSED：值为3，表示连接关闭，或连接失败
```
switch (ws.readyState) {
  case WebSocket.CONNECTING:
    // do something
    break;
  case WebSocket.OPEN:
    // do something
    break;
  case WebSocket.CLOSING:
    // do something
    break;
  case WebSocket.CLOSED:
    // do something
    break;
  default:
    // this never happens
    break;
}
```

**4.3 webSocket.onopen**
指定连接成功后的回调函数
```
//单个回调
ws.onopen = function(){
    ws.send('Hello Server!')
}

//多个回调
ws.addEventListener('open',function(event){
    ws.send('Hello Server!')
})
```

**4.4 webSocket.onclose**
用于指定关闭后的回调函数
```
ws.onclose = function(event) {
  var code = event.code;
  var reason = event.reason;
  var wasClean = event.wasClean;
  // handle close event
};

ws.addEventListener("close", function(event) {
  var code = event.code;
  var reason = event.reason;
  var wasClean = event.wasClean;
  // handle close event
});
```

**4.5 webSocket.onmessage**
用于指定收到服务器数据后的回调函数
```
ws.onmessage = function(event) {
  var data = event.data;
  // 处理数据
};

ws.addEventListener("message", function(event) {
  var data = event.data;
  // 处理数据
});
```

**4.6 webSocket.send()**
用于向服务器发送数据
```
//发送文本
ws.send('your message!');

//发送Blob对象
var file = document
  .querySelector('input[type="file"]')
  .files[0];
ws.send(file);
```

**4.7 webSocket.bufferedAmount**
表示还有多少字节的二进制数据没有发送出去。可判断发送是否结束。
```
var data = new ArrayBuffer(10000000);
socket.send(data);

if (socket.bufferedAmount === 0) {
  // 发送完毕
} else {
  // 发送还没结束
}
```

**4.8 webSocket.onerror**
用于指定报错时的回调函数
```
socket.onerror = function(event) {
  // handle error event
};

socket.addEventListener("error", function(event) {
  // handle error event
});
```

#### 5.WebSocket服务器
webSocket协议需要服务器支持。

## 完结 2019/9/5
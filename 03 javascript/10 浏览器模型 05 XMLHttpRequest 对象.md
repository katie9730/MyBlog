#### 1.简介     
浏览器与服务器之间，采用HTTP协议通信。用户在浏览器地址栏键入一个网址，或者通过网页表单向服务器提交内容，这时浏览器就会向服务器发出HTTP请求。    
具体来说，AJAX包括以下几个步骤：
+ 1. 创建XMLHttpRequest实例
+ 2. 发出HTTP请求
+ 3. 接受服务器传回的数据
+ 4. 更新网页数据   
  
XMLHttpRequest对象是AJAX的主要接口，用于浏览器与服务器之间的通信。尽管名字里面有XML和HTTP，不过实际上可以使用多种协议（比如file或者ftp）,发送任何格式的数据。
    
XMLHttpRequest本身是一个构造函数，可以使用new命令来生成实例。没有任何参数。
```
var xhr = new XMLHttpRequest();
//一旦新建实例，就可以使用open()方法发出HTTP请求。
xhr.open('GET','http://www.example.com/page.php',true);
//上面代码向指定的服务器网址，发出GET请求。
//然后指定回调函数，监听通信状态（readyState属性）的变化。
xhr.onreadystatechange = handleStateChange;
function handleStateChange(){
    //...
}
//一旦XMLHttpRequest实例的状态发生变化，就会调用监听函数handleStateChange。
```   
注意：AJAX只能向同源网址（协议、域名、端口相同）发出HTTP请求，如果发生跨域请求，就会报错

#### 2.XMLHttpRequest的实例属性
**2.1 XMLHttpRequest.readyState**
返回一个整数，表示实例对象的当前状态。属性为只读
+ 0：表示XMLHttpRequest实例已经生成，但是实例的open()方法没有被调用。
+ 1：open()方法已经调用，实例的send()没有调用，仍然可以使用实例的setRequestHeader()方法，设定HTTP请求的头信息。
+ 2：send()方法已经调用，并且服务器返回的头信息和状态码已经收到。
+ 3：表示正在接收服务器传来的数据体（body部分）。这时，实例的responseType属性等于text或者是空字符串，responseText属性就会包含已经收到的部分信息。
+ 4：表示服务器返回的数据完全接收，或者本次接收已经失败。 

**2.2 XMLHttpRequest.onreadystatechange**   
指向一个监听函数。readystatechange事件发生时（实例的readyState属性变化），就会执行这个属性。另外，如果使用实例的abort()方法，终止XMLHttpRequest请求，也会造成readyState属性变化，导致调用XMLHttpRequest.onreadystatechange属性。

**2.3 XMLHttpRequest.response** 表示服务器返回的数据体。属性为只读。若请求没有成功或者数据不完整，该属性等于null。

**3.4 XMLHttpRequest.responseType**   
属于一个字符串，表示服务器返回数据的类型。这个属性的值，告诉服务器返回指定类型的数据。如果responseType设为空字符串，就等同于默认值text。 

**2.5 XMLHttpRequest.responseText**    
从服务器接收到的字符串，该属性为只读。只有HTTP请求完成接受后，该属性才会包含完整的数据。

**2.6 XMLHttpRequest.responseXML**  
该属性返回从服务器接收到的HTML或XML文档对象，该属性为只读。如果本次请求没有成功，或者收到的数据不能被解析为XML或HTML，该属性等于Null。

**2.7 XMLHttpRequest.responseURL**   
该属性是字符串，表示发送数据的服务器的网址。注意，该属性的值与open()方法指定的请求网址不一定相同。

**2.8 XMLHttpRequest.status,XMLHttpRequest.statusText**  
XMLHttpRequest.status属性返回一个整数，表示服务器会的HTTP状态码。若通信成功的话，该状态码为200；若没有状态码返回，默认也是200。
+ 200:ok，访问正常
+ 301, Moved Permanently，永久移动
+ 302, Moved temporarily，暂时移动
+ 304, Not Modified，未修改
+ 307, Temporary Redirect，暂时重定向
+ 401, Unauthorized，未授权
+ 403, Forbidden，禁止访问
+ 404, Not Found，未发现指定网址
+ 500, Internal Server Error，服务器发生错误   


**2.9 XMLHttpRequest.timeout,XMLHttpRequestEventTarget.ontimeout**    
+ XMLHttpRequest.timeout属性返回一个整数，表示多少毫秒后，如果请求仍然没有得到结果，就会自动终止。如果属性等于0，表示没有时间限制。    
+ XMLHttpRequestEventTarget.ontimeout属性用于设置一个监听函数，如果发生timeout事件，就会执行这个监听函数。

**2.10 事件监听属性**    
XMLHttpRequest对象可以对以下事件指定监听函数。   
+ XMLHttpRequest.onloadStart：loadstart事件（HTTP请求发出）的监听函数。
+ XMLHttpRequest.onprogress：progress事件（正在发送和加载数据）的监听函数。
+ XMLHttpRequest.onabort:abort事件（请求中止）的监听函数。
+ XMLHttpRequest.onerror：error 事件（请求失败）的监听函数
+ XMLHttpRequest.onload：load 事件（请求成功完成）的监听函数
+ XMLHttpRequest.ontimeout：timeout 事件（用户指定的时限超过了，请求还未完成）的监听函数
+ XMLHttpRequest.onloadend：loadend 事件（请求完成，不管成功或失败）的监听函数  
## 未完待续 2019/6/24

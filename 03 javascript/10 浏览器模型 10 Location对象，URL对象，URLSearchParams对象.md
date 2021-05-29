#### 1.Location对象
是浏览器的原生对象,用于提供URL相关的信息和操作。通过window.location和document.location可以拿到这个对象。

**1.1 属性**
+ Location.href:整个URL(只有此属性是浏览器唯一允许跨域写入的属性，其他都不可以)
+ Location.protocol：当前URL的协议，包括冒号
+ Location.host：主机和端口号
+ Location.hostname：主机名，不包括端口
+ Location.port：端口号
+ Location.pathname：URL的路径部分，从根路径/开始
+ Location.search：查询字符串部分，从问好？开始
+ Location.hash：片段字符串部分，从#开始
+ Location.username：域名前面的用户名
+ Location.password：域名前面的密码
+ Location.origin：URL的协议、主机名和端口(只有此属性为只读，其他都为可写)

```
document.location = 'http://www.example.com'
// 等同于。直接改写location，相当于写入href属性。
document.location.href = 'http://www.example.com'
```

**1.2 方法**
+ Location.assign()：接受一个URL字符串作为参数。成功则跳转，失败则报错
+ Location.replace()：与Location.assign相同，不同在于它用新URL替换了老的URL。
+ 1.3 Location.reload()：接受布尔值作为参数。使得浏览器重新加载当前网址，相当于刷新按钮。
+ 1.4 Location.toString()：类似Location.href属性，返回整个URL字符串。

#### 2.URL的编码和解码
网页的URL只能包含合法的字符，合法字符有URL元字符和语义字符。除了以上两类字符，其他字符出现在URL之中则需转义。
JavaScript提供了四种URL的编码/解码方法。
**2.1 encodeURI() 编码**
用于转码整个URL。参数为字符串，代表整个URL
```
encodeURI('http://www.example.com/q=春节')
// "http://www.example.com/q=%E6%98%A5%E8%8A%82"
```
**2.2 encodeURIComponent() 编码**
用于转码URL的组成部分。除语义字符外的所有字符。接受一个参数，则是URL的片段。
```
encodeURIComponent('春节')
// "%E6%98%A5%E8%8A%82"
encodeURIComponent('http://www.example.com/q=春节')
// "http%3A%2F%2Fwww.example.com%2Fq%3D%E6%98%A5%E8%8A%82"
```
**2.3 decodeURI() 解码**
用于整个URL的解码，是encodeURI()方法的逆运算。
**2.4 decodeURIComponent() 解码**
用于URL片段的解码。是encodeURIComponent()方法的逆运算。

#### 3.URL对象
是浏览器的原生对象，可用来构造、解析和解码URL。一般可通过window.URL可以拿到这个对象。

**3.1 构造函数**
+ URL对象本身是一个构造函数，可生产URL实例。
```
var url = new URL('http://www.example.com/index.html')
url.href
// "http://www.example.com/index.html"
```
+ 如果参数是另一个URL实例，则构造函数会自动读取实例的href属性，作为实际参数。
+ 如果URL字符串是一个相对路径，则需要表示绝对路径的第二个参数，作为计算基准。

**3.2 实例属性**
URL实例的属性与Location对象的属性基本一致，返回当前URL的信息。
+ URL.href：返回整个URL
+ URL.protocol：返回协议，以冒号结尾
+ URL.hostname：返回域名
+ URL.host：返回域名与端口，包含冒号，默认的80,443端口省略
+ URL.port：返回端口
+ URL.origin：返回协议、域名和端口
+ URL.pathname：返回路径，以斜杠/开头
+ URL.search：返回查询字符串，以问号？开头
+ URL.searchParams：返回一个URLSearchParams实例，该属性是Location对象没有的
+ URL.hash：返回片段识别符，以#开头
+ URL.password：返回域名前面的密码
+ URL.username：返回域名前面的用户名

**3.3 静态方法**
+ URL.createObjectURL()：用于上传/下载文件、流媒体文件生产一个URL字符串。该字符串代表File对象或Blob对象的URL
```
var div = document.getElementById('display');
function handleFiles(files){
    for (var i = 0; i < files.length; i++){
        var img = ducument.createElement('img');
        img.src = window.URL.createObjectURL(files[i])
        div.appendChild(img)
    }
}
```
+ URL.revokeObjectURL：用于释放URL.createObjectURL方法生成的URL实例。他的参数是URL.createdObjectURL方法返回的URL字符串。

#### 4.URLSearchParams对象
**4.1 概述**
是浏览器的原生对象，用来构造、解析和处理URL的查询字符串（即URL问号后面的部分）。
```
// 方法一：传入字符串
var params = new URLSearchParams('?foo=1&bar=2');
// 等同于
var params = new URLSearchParams(document.location.search);

// 方法二：传入数组
var params = new URLSearchParams([['foo', 1], ['bar', 2]]);

// 方法三：传入对象
var params = new URLSearchParams({'foo' : 1 , 'bar' : 2});
```
**4.2 URLSearchParams.toString()**
返回实例的字符串形式
```
var url = new URL('https://example.com?foo=1&bar=2');
var params = new URLSearchParams(url.search);
params.toString()  //'foo=1&bar=2'
```
**4.3 URLSearchParams.append()**
用来追加一个查询参数。接受两个参数，第一个为键名，第二个为键值，没有返回值。
```
var params = new URLSearchParams({'foo':1, 'bar':2});
params.append('bax',3);
params.toString()  //'foo=1&bar=2&baz=3'
```
**4.4 URLSearchParams.delete()**
用来删除指定的查询参数，接受键名作为参数
```
var params = new URLSearchParams({'foo': 1 , 'bar': 2});
params.delete('bar');
params.toString()  //'foo=1'
```
**4.5 URLSearchParams.has()**
返回布尔值，表示查询字符串是否包含指定的键名
```
var params = new URLSearchParams({'foo': 1 , 'bar': 2});
params.has('bar')  //true
params.has('baz')  //false
```
**4.6 URLSearchParams.set()**
用来设置查询字符串的键值。接受两个参数：键名，键值。已存在的键，则键值被改写，否则为追加。
```
var params = new URLSearchParams('?foo=1');
params.set('foo', 2);
params.toString() // "foo=2"
params.set('bar', 3);
params.toString() // "foo=2&bar=3"
```
**4.7 URLSearchParams.get(),URLSearchParams.getAll()**
用来读取查询字符串里面的指定键。接受一个参数：键名。
```
var params = new URLSearchParams('?foo=1');
params.get('foo') // "1"
params.get('bar') // null
//注意1:键值返回的是字符串
//注意2:键名不存在，返回值为null
//注意3:存在多个同名键，get返回的是最前面的键值

var params = new URLSearchParams('?foo=1&foo=2');
params.getAll('foo') // ["1", "2"]
返回一个数组，接受键名最为参数
```
**4.8 URLSearchParams.sort()**
对查询字符串里面的键进行排序，规则按照Unicode码点从小到大排序。没有返回值或者是undefined。
```
var params = new URLSearchParams('c=4&a=2&b=3&a=1');
params.sort();
params.toString() // "a=2&a=1&b=3&c=4"
```
**4.9 URLSearchParams.keys(),URLSearchParams.values(),URLSearchParams.entries**
返回一个遍历器对象，共for...of循环遍历。 区别在于  
+ keys方法返回的是键名的遍历器
+ values方法返回的是键值对的遍历器
+ entries返回的是键值对的遍历器
```
var params = new URLSearchParams('a=1&b=2');

for(var p of params.keys()) {
  console.log(p);
}
// a
// b

for(var p of params.values()) {
  console.log(p);
}
// 1
// 2

for(var p of params.entries()) {
  console.log(p);
}
// ["a", "1"]
// ["b", "2"]
```
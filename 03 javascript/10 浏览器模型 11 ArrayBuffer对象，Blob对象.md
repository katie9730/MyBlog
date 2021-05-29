#### 1.ArrayBuffer对象（ES6引入，此处仅简略介绍）
ArrayBuffer对象表示一段二进制数据，用来模拟内存中的数据。     
浏览器原生提供ArrayBuffer()构造函数，用来生成实例。接受一个整数作为参数，表示占用的字节。
```
var buffer = new ArrayBuffer(8);

//可通过byteLength属性，读取内存长度
buffer.byteLength //8

//可通过slice方法，进行复制一部分内存
var buf1 = new ArrayBuffer(8)
var buf2 = buf1.slice(0);

```

#### 2.Blob对象
**2.1 简介**   
表示一个二进制文件的数据内容。Blob用于操作二进制文件，ArrayBuffer用于操作内存。     
浏览器原生提供Blob()构造函数，用来生成实例。接受两个参数,第一个参数为数组，成员为字符串或二进制对象，表示新生成的Blob实例对象内容;第二个参数可选，为配置对象，目前只有一个属性type，值为字符串，表示数据的MIME类型，默认是空字符串。
```
var htmlFragment = ['<a id="a"><b id="b">hey!</b></a>'];
var myBlob = new Blob(htmlFragment, {type : 'text/html'});
```

**2.2 实例属性和实例方法**
+ Blob具有两个实例属性size和type，分别返回数据的大小和类型。
+ Blob具有一个实例方法slice，用来拷贝原来的数据，返回的也是一个Blob实例。
```
var htmlFragment = ['<a id="a"><b id="b">hey!</b></a>'];
var myBlob = new Blob(htmlFragment, {type : 'text/html'});
myBlob.size // 32
myBlob.type // "text/html"

myBlob.slice(start，end, contentType)
```

**2.3 获取文件信息**   
文件选择器`<input type='file'>`用来让用户选取文件。此选择器不允许自行设置value属性，而是选择成功，脚本自己读取。     
文件选择器返回一个FileList对象（类似数组），成员为File实例对象（也是特殊的Blob实例），增加胃name和lastModifiedDate属性。
```
function fileinfo(files) {
  for (var i = 0; i < files.length; i++) {
    var f = files[i];
    console.log(
      f.name, // 文件名，不含路径
      f.size, // 文件大小，Blob 实例属性
      f.type, // 文件类型，Blob 实例属性
      f.lastModifiedDate // 文件的最后修改时间
    );
  }
}
```

**2.4 下载文件**    
AJAX请求时，responseType属性为blob时，下载下来就是一个Blob对象。
```
function getBlob(url, callback){
    var xhr = new XMLHttpRequest();
    xhr.open('Get', url);
    xhr.responseType = 'blob';
    xhr.onload = function(){
        callBack(xhr.response);
    }
    xhr.send(null);
}
```

**2.5 生成URL**    
使用URL.createObjectURL()方法，针对Blob对象生产一个临时URL。以blob://开头，表明对应Blob对象，协议头后面为一个标识符，用来对应内存中的Blob对象。 浏览器处理 Blob URL 就跟普通的 URL 一样，如果 Blob 对象不存在，返回404状态码；如果跨域请求，返回403状态码。Blob URL 只对 GET 请求有效，如果请求成功，返回200状态码。由于 Blob URL 就是普通 URL，因此可以下载。

**2.6 读取文件**   
取得Blob对象后，通过FileReader对象，读取Blob对象的内容，即文件内容。   
FileReader 对象提供四个方法，处理 Blob 对象。
+ FileReader.readAsText()：返回文本，需要指定文本编码，默认为 UTF-8。
+ FileReader.readAsArrayBuffer()：返回 ArrayBuffer 对象。
+ FileReader.readAsDataURL()：返回 Data URL。
+ FileReader.readAsBinaryString()：返回原始的二进制字符串。

## 完结 2019/9/5
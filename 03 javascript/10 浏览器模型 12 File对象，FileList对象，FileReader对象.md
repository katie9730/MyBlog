#### 1.File对象    
File对象代表一个文件，用来读写文件信息。且继承了Blob对象。

**1.1 构造函数**
浏览器原生提供一个File()构造函数，用来生成File实例对象。接受三个参数
+ array：一个数组，表示文件的内容
+ name：字符串，表示文件名或文件路径
+ options：配置对象，设置实例的属性type（字符串）和lastModified（时间戳）

**1.2 实例属性和实例方法**
+ File.lastModified：最后修改时间
+ File.name：文件名或文件路径
+ File.size：文件大小（单位字节）
+ File.type：文件的 MIME 类型

#### 2.FileList对象
类似数组的对象，代表一组选中的文件，每个成员都是一个File实例。主要出现在两个场合。
+ 文件控件节点（<input type="file">）的files属性，返回一个 FileList 实例。
+ 拖拉一组文件时，目标区的DataTransfer.files属性，返回一个 FileList 实例。

#### 3.FileReader对象
用于读取File对象或Blob对象所包含的文件内容。  
浏览器原生提供一个FileReader构造函数，用来生成FileReader实例。
```
var reader = new FileReader();
```
**FileReader 有以下的实例属性**
+ FileReader.error：读取文件时产生的错误对象
+ FileReader.readyState：整数，表示读取文件时的当前状态。一共有三种可能的状态，0表示尚未加载任何数据，1表示数据正在加载，2表示加载完成。
+ FileReader.result：读取完成后的文件内容，有可能是字符串，也可能是一个 ArrayBuffer 实例。
+ FileReader.onabort：abort事件（用户终止读取操作）的监听函数。
+ FileReader.onerror：error事件（读取错误）的监听函数。
+ FileReader.onload：load事件（读取操作完成）的监听函数，通常在这个函数里面使用result属性，拿到文件内容。
+ FileReader.onloadstart：loadstart事件（读取操作开始）的监听函数。
+ FileReader.onloadend：loadend事件（读取操作结束）的监听函数。
+ FileReader.onprogress：progress事件（读取操作进行中）的监听函数。

**FileReader有以下实例方法**
+ FileReader.abort()：终止读取操作，readyState属性将变成2。
+ FileReader.readAsArrayBuffer()：以 ArrayBuffer 的格式读取文件，读取完成后result属性将返回一个 ArrayBuffer 实例。
+ FileReader.readAsBinaryString()：读取完成后，result属性将返回原始的二进制字符串。
+ FileReader.readAsDataURL()：读取完成后，result属性将返回一个 Data URL 格式（Base64 编码）的字符串，代表文件内容。对于图片文件，这个字符串可以用于<img>元素的src属性。注意，这个字符串不能直接进行 Base64 解码，必须把前缀data:*/*;base64,从字符串里删除以后，再进行解码。
+ FileReader.readAsText()：读取完成后，result属性将返回文件内容的文本字符串。该方法的第一个参数是代表文件的 Blob 实例，第二个参数是可选的，表示文本编码，默认为 UTF-8。

## 完结 2019/9/5
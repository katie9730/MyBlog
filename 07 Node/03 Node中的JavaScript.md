## 1.Node.js是什么
是JavaScript运行时，既不是语言也不是框架，而是一个平台。

## 2.Node中的JavaScript
- EcmaScript（没有DOM、BOM）
    + 变量
    + 方法
    + 数据类型
    + 内置对象
    + Array
    + Object
    + Date
    + Math
- 核心模块
    + 在Node中没有全局作用域的概念
    + 在Node中，只能通过require方法来加载执行多个JavaScript脚本文件
    + require加载只能是执行其中的代码，文件与文件之间由于有模块作用域，所以不会有污染的问题。
        * 模块完全是封闭的
        * 外部无法访问内部
        * 内部也无法访问外部
        *
    + 模块作用域固然带来了一些好处，可以加载执行多个文件，可以完全避免变量命名冲突污染的问题
    + 但是某些情况下，模块与模块是需要进行通信的
    + 在每个模块中，都提供了一个对象：exports
    + 该对象默认是一个空对象
    + 你要做的就是把需要被外部访问使用的成员手动的挂载到 exports 接口对象中
    + 然后谁来 require 这个模块，谁就可以得到模块内部的 exports 接口对象
    + 还有其它的一些规则，具体后面讲，以及如何在项目中去使用这种编程方式，会    + 通过后面的案例来处理
- 核心模块
    + 核心模块是由 Node 提供的一个个的具名的模块，它们都有自己特殊的名称标识，例如
        - fs 文件操作模块
        - http 网络服务构建模块
        - os 操作系统信息模块
        - path 路径处理模块
        - ...
    + 所有核心模块在使用的时候都必须手动的先使用 require 方法来加载，然后才可以使用，例如：`var fs = require('fs')`
- http
    + require
    + 端口号
        * ip地址定位计算机
        * 端口号定位具体的应用程序
    + Content-Type
        * 服务器最好把每次响应的数据是什么内容类型都告诉客户端，而且要正确的告诉
        * 不同的资源对应的 Content-Type 是不一样，具体参照：http://tool.oschina.net/commons
        * 对于文本类型的数据，最好都加上编码，目的是为了防止中文解析乱码问题
    + 通过网络发送文件
        * 发送的并不是文件，本质上来讲发送是文件的内容
        * 当浏览器收到服务器响应内容之后，就会根据你的 Content-Type 进行对应的解析处理
- 模块系统
- Node中的其他的核心模块
- Express Web开发框架
    + npm install express


> Node为JavaScript提供了很多服务器级别的API，这些API绝大多数都被包装到了一个具名的核心模块中了。例如文件操作的`fs`核心模块，http服务构建的`http`模块，`path`路径操作模块，`os`操作系统信息模块等
> 只要说到这是一个核心模块，就得知道要用`require`引用它。`var fs = require('fs')`

```
//用来获取文件模块的
var fs = require('fs')

//用来获取URL
qs.parse():将URL解析成对象的形式
qs.stringify():将对象序列化成URL的形式，以&进行拼接

//用来获取机器信息的
var os = require('os')

//用来操作路径的
var path = require('path')

//获取当前机器的cpu机器
console.log(os.cpus())

//memory 内存
console.log(os.totalmem())

//extname = extension name
console.log(path.extname('c:/a/b/c/d/hello.txt'))

```
- 第三方模块
- 用户自定义模块
> a.js如下
```
// require是一个方法
// 它的作用就是用来加载模块的
// 在Node中，模块有三种
//      具名的核心模块，例如fs、http
//      用户自己编写的文件模块
//          相对路径必须加 ./
//          可以省略后缀名
//          相对路径中的 ./不能省略，否则会报错
//      在Node中，没有全局作用域，只有模块作用域
//          外部访问不到内部
//          内部也访问不到外部
//          默认都是封闭的
//      既然是模块作用域，那如何让模块与模块之间进行通信
//      有时候，我们加载文件模块的目的不是为了简简单单的执行里面的代码，更重要的是为了使用里面的某种方法
// require 方法有两个作用
//      1.加载文件模块并执行里面的代码
//      2.拿到被加载文件模块导出的接口对象
//
//      在每个文件模块中都提供了一个对象：exports
//      exports默认是一个空对象
//      你要做的就是把所有需要被外部访问的成员挂载到exports对象中
//      eg: var foo = 'bbb'
//          exports.foo = 'hello'
var fs = require('fs');
//作用一
console.log('a start')
require('./b.js')
console.log('a end')

////作用二
var bExports = require('./b')
console.log(bExports.foo)
console.log(bExports.age)
console.log(bExports.add(10,30))
bExports.readFile('./a.js')
fs.readFile('./a.js',function(err,data){
    if(err){
        console.log('读取文件失败')
    }else{
        console.log(data.toString())
    }
})

```
> b.js如下
```
//作用一
console.log('b.js文件被加载执行了')

//作用二
var foo = 'bbb';
exports.foo = 'hello';
var age = 18;
exports.age = age;
exports.add = function(x,y){
    return x+y
}
exports.readFile = function(path,callback){
    console.log('文件路径：', path);
}

```
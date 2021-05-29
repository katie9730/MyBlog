#### 1.概念    
webpack的配置文件，是导出一个对象的JavaScript文件。此对象，由webpack根据对象定义的属性进行解析。    
因为webpack配置是标准的Node.js CommonJS模块，所以可以做到以下事情：
+ 通过require(...)导入其他文件
+ 通过require(...)使用npm的工具函数
+ 使用JavaScript控制流表达式，例如`?:`操作符
+ 对常用值使用常量或变量
+ 编写并执行函数来生成部分配置     

虽然技术上可行，但应避免以下做法：

+ 在使用 webpack 命令行接口(CLI)（应该编写自己的命令行接口(CLI)，或使用 --env）时，访问命令行接口(CLI)参数
+ 导出不确定的值（调用 webpack 两次应该产生同样的输出文件）
+ 编写很长的配置（应该将配置拆分为多个文件）

#### 2.基本配置
```
[webpack.config.js文件]
var path = require('path');

module.exports = {
    mode:'development',
    entry:'./foo.js',
    output:{
        path:path.resolve(__dirname,'dist'),
        filename:'foo.bundle.js'
    }
}

```
#### 1.用法
要设置 target 属性，只需要在你的 webpack 配置中设置 target 的值。
```
module.exports = {
    target:'node'
}
```
多个Target
```
var path = require('path');
var serverConfig = {
    target:'node',
    output:{
        path:path.resolve(__dirname,'dist'),
        filename:'lib.node.js'
    }
}

var clientConfig = {
    target:'web',
    output:{
        path:path.resolve(__dirname,'dist'),
        filename:'lib.js'
    }
}

module.exports = [serverConfig,clientConfig]

```
#### 1.概述
插件时webpack的支柱功能。webpack自身也是构建于，你在webpack配置中用到的相同的插件系统之上！插件目的在于解决loader无法实现的其他事。

#### 2.剖析
webpack插件是一个具有apply属性的JavaScript对象。apply属性会被webpack compiler调用，并且compiler对象可在整个编译生命周期访问。

### 3.用法
插件可以携带参数/选项。必须在webpack配置中，向plugins属性传入new实例。
**3.1 配置**
```
[webpack.config.js文件]
const HtmlWebpackPlugin = require('html-webpack-plugin');   //通过npm安装
const webpack = require('webpack');  //访问内置插件
const path = require('path');

const config = {
    entry:'./path/to/my/entry/file.js',
    output:{
        filename:'my-first-webpack.bundle.js',
        path:path.resolve(__dirname,'dist')
    },
    module:{
        rules:[
            {
                test:/\.(js|jsx)$/,
                use：'babel-loader'
            }
        ]
    },
    plugins:[
        new webpack.optimize.UglifyJsPlugin(),
        new HtmlWebpackPlugin({template:'./src/index.html'})
    ]
}

modele.exports = config;

```

**3.2 Node API**
即便使用 Node API，用户也应该在配置中传入 plugins 属性。compiler.apply 并不是推荐的使用方式。
```
[some-node-script.js文件]
const webpack = require('webpack'); //访问 webpack 运行时(runtime)
const configuration = require('./webpack.config.js');

let compiler = webpack(configuration);
compiler.apply(new webpack.ProgressPlugin());

compiler.run(function(err, stats) {
// ...
});
```
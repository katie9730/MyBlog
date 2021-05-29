#### 1.概述   
loader用于对模块的源代码进行转换。loader可以使你在import或‘加载’模块时预处理文件。因此，loader类似于其他构建工具中‘任务（task）’，并提供了处理前端构建步骤的强大方法。loader可以将文件从不同的语言（如TypeScript）转换为JavaScript，或将内联图像转换为data URL。loader甚至允许你直接在JavaScript模块中`import`css文件！

#### 2.示例
若想让loader告诉webpack加载css文件，或将TypeScript转为JavaScript。首先得先安装对应的loader
```
npm install --save-dev css-loader
npm install --save-dev ts-loader
```
然后指示wabpack对每个.css使用css-loader，以及对所有.ts文件使用ts-loader
```
[webpack.config.js文件]
module.exports = {
    module:{
        rules:[
            {test:/\.css$/,use:'css-loader'},
            {test:/.ts/,use:'ts-loader'}
        ]
    }
};

```
#### 3.使用loader
+ 配置（推荐）：在webpack.config.js文件中指定loader
+ 内联：在每个import语句中显式指定loader
+ CLI：在shell命令中指定它们

**3.1配置[configuration]**   
module.rules允许你在webpack配置中指定多个loader。
```
module:{
    rules:[
    {
        test:/\.css$/,
        use:[
            {loader：'style-loader'},
            {
                loader:'css-loader',
                options:{
                    modules:true
                }
            }
        ]
    }
    ]
}
```

**3.2 内联**
可以在import语句或任何等效于‘import’的方式中指定loader。使用`!`将资源中的loader分开。分开的每个部分都相对于当前目录解析。
```
import Styles from 'style-loader!css-loader?modules!./styles.css';
```

**3.3 CLI**
```
webpack --module-bind jade-loader --module-bind 'css=style-loader!css-loader'
//这会对 .jade 文件使用 jade-loader，对 .css 文件使用 style-loader 和 css-loader。
```

#### loader特性
+ loader 支持链式传递。能够对资源使用流水线(pipeline)。一组链式的 loader 将按照相反的顺序执行。loader 链中的第一个 loader 返回值给下一个 loader。在最后一个 loader，返回 webpack 所预期的 JavaScript。
+ loader 可以是同步的，也可以是异步的。
+ loader 运行在 Node.js 中，并且能够执行任何可能的操作。
+ loader 接收查询参数。用于对 loader 传递配置。
+ loader 也能够使用 options 对象进行配置。
+ 除了使用 package.json 常见的 main 属性，还可以将普通的 npm 模块导出为 + loader，做法是在 package.json 里定义一个 loader 字段。
+ 插件(plugin)可以为 loader 带来更多特性。
+ loader 能够产生额外的任意文件。

#### 解析loader    
loader遵循标准的模块解析。多数情况下，loader将从模块路径（通常将模块路径认为是npm install，node_modules）解析。    
loader模块需要导出一个函数，并且使用Node.js兼容的JavaScript编写。通常使用npm进行管理，但是也可以将自定义loader作为应用程序的文件。loader通常被命名为xxx-loader。
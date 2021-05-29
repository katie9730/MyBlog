如何去配置entry属性

#### 1.单个入口(简写)语法    
用法：entry：string|Array<string>
```
[webpack.config.js文件]

const config = {
    entry: './path/to/my/entry/file.js'
}

module.exports = config;


//这是简写方式
const config = {
    entry:{
        main: './path/to/my/entry/file.js'
    }
}

```

#### 2.对象语法    
用法:entry:{[entryChunkName:string]:string|Array<string>}
```
[webpack.config.js文件]
const config = {
    entry:{
        app:'./src/app.js',
        vendors:'./src/vendors.js'
    }
}
```
对象语法会比较繁琐。然而，这是应用程序中定义入口的最可扩展的方式。
> "可扩展的webpack配置"是指，可重用并且可以与其他配置组合使用。这是一种流行的技术，用于将关注点（concern）从环境（environment）、构建目标（build target）、运行时(runtime)中分离。然后使用专门的工具（如webpack-merge）将他们合并。

#### 3.常见场景
**3.1分离应用程序（app）和第三方库（vendor）入口**
```
[webpack.config.js文件]
const config = {
    entry:{
        app:'./src/app.js',
        vendors:'./src/vendors.js'
    }
}
```
这告诉我们 webpack 从 app.js 和 vendors.js 开始创建依赖图(dependency graph)。这些依赖图是彼此完全分离、互相独立的（每个 bundle 中都有一个 webpack 引导(bootstrap)）。这种方式比较常见于，只有一个入口起点（不包括 vendor）的单页应用程序(single page application)中。    
**3.2多页面应用程序**
```
[webpack.config.js文件]
const config = {
    entry:{
        pageOne:'./src/pageOne/index.js',
        pageTWO:'./src/pageTwo/index.js',
        pageThree: './src/pageThree/index.js'
    }
}
```
在多页应用中，（译注：每当页面跳转时）服务器将为你获取一个新的 HTML 文档。页面重新加载新文档，并且资源被重新下载。然而，这给了我们特殊的机会去做很多事：

使用 CommonsChunkPlugin 为每个页面间的应用程序共享代码创建 bundle。由于入口起点增多，多页应用能够复用入口起点之间的大量代码/模块，从而可以极大地从这些技术中受益。
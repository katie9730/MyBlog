控制webpack如何向硬盘写入编译文件。注意即使存在多个入口文件，但只指定一个输出配置。

#### 1.用法(Usage)
最基本用法，将它的值设置为一个对象，包括以下两点：
+ `filename`用于输出文件的文件名
+ `path`作为目标输出目录的绝对路径
```
const config = {
    output:{
        filename:'bundle.js',
        path:'/home/proj/public/assets'
    }
}

module.exports = config;
```

#### 2.多个入口起点   
如果配置创建多个单独的‘chunk’，则使用占位符来确保每个文件具有唯一的名称。
```
[webpack.config.js文件]
{
    entry:{
        app:'./src/app.js',
        search:'./src/search.js'
    },
    output:{
        filename:'[name].js',
        path:__dirname + '/dist'
    }
}

//写入到硬盘：./dist/app.js, ./dist/search.js
```

#### 3.高级进阶
```
[config.js文件]
output:{
  path: "/home/proj/cdn/assets/[hash]",
  publicPath: "http://cdn.example.com/assets/[hash]/"
}
```
在编译时不知道最终输出文件的 publicPath 的情况下，publicPath 可以留空，并且在入口起点文件运行时动态设置。如果你在编译时不知道 publicPath，你可以先忽略它，并且在入口起点设置 __webpack_public_path__。
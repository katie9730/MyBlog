- 初始化npm环境
    + node -v和npm -v查看版本
    + 进入项目目录，npm init初始化项目，最终生成package.json文件。
- 安装插件
    + 使用webpack作为构建工具。安装插件`npm install webpack webpack-dev-server --save -dev`
    + 安装React插件`npm i react react-dom save`。
    + 安装完成之后，查看package.json中多了`devDependencies`和`dependencies`两项。根目录也多了`node_modules`文件夹。
- `--save`与`--save-dev`的区别
    + `--save`依赖插件记录到dependencies中。该插件是在项目运行时必须依赖的插件。
    + `--save-dev`依赖插件记录到devDependencies中。 记录项目在开发过程中使用的插件。
- 文件夹功能简述
    + app:所有的代码在此处
    + build:编译出来的发布文件
    + docs:是目录
    + mock:模拟数据
    + node_modules:npm安装的插件
- app/index.jsx[入口文件]
    + entry:为入口文件
    + output:输出文件
- 配置webpack.production.config.js
> 开发环境下，可以不用考虑系统的行能，更多考虑的是如何增加开发效率。而发布系统时，就需要考虑发布之后的系统的性能，包括加载速度、缓存等。下面介绍发布用配置代码和开发用的不一样的地方。
- 发布到`./build`文件夹中
> `path:__dirname + '/build'`

- vendor
> 将第三方依赖单独打包。即将node_modules文件夹中的代码打包为vendor.js将我们自己写的业务代码打包为app.js。这样有助于缓存，因为在项目维护过程中，第三方依赖不经常变化，而业务代码会经常变化。

- md5后缀
> 为每个打包出来的文件都加md5后缀，例如`"/js/[name].[chunkhash:8].js"`,可使文件强缓存。

- 分目录
> 打包出来的不同类型的文件，放在不同目录虾，例如图片文件将放在`img/`目录下。
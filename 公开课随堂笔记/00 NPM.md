### 1.NPM介绍
npm是与node.js一起安装的包管理工具，用来解决node.js代码部署上的问题。

#### 1.1使用npm命令安装模块
```
npm install <Module Name>
// 安装好之后，模块包会放在node_modules目录中，通过require('express')引入
```

#### 1.2 全局安装(含有`-g`)与本地安装
+ 本地安装：将安装包放在`./node_modules`下，通过require()引入本地安装的包。
+ 全局安装：将安装包放在`/user/local`下或者node的安装目录中。

#### 1.3 查看安装信息
+ 查看安装信息：npm list -g
+ 查看模块: npm list <模块名称>，例如`npm list grunt`

#### 1.4 package.json
package.json位于模块的目录下，用于定义包的属性。

```
npm uninstall express  // 卸载express模块
npm ls // 卸载后查看包是否存在
npm update express // 更新模块
npm search express // 搜索模块
npm init // 初始化模块
npm publish // 发布模块
npm help // 查看所有命令
npm cache clear // 清空NPM本地缓存，使用场景是使用相同版本号发布新版本代码的时候
npm unpublish <package>@<version> // 撤销发布过的某个版本代码
```


### 2.第三方模块总结罗列
#### serve
+ 安装`npm i serve --save`
+ 使用`serve -s build`
+ 介绍：前端打好包后有时需要将打包好的项目跑一下看看效果，但又不能直接打开，这时可以使用seve工具。即可查看打包好的项目。
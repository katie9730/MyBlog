```
介绍
基于Nodejs的自动任务运行器， 她能自动化地完成javascript/coffee/sass/less/html/image/css 等文件的的测试、检查、合并、压缩、格式化、浏览器自动刷新、部署文件生成，并监听文件在改动后重复指定的这些步骤。

命令
gulp watch:每次修改LESS文件之后，它会自动帮你编译一次，可直接刷新浏览器看到新的效果。

安装对应的gulp插件
1.进入控制台：node
2.安装gulp-less插件：npm install gulp-less  (用于编译less)
3.安装gulp-concat插件：npm install gulp-concat  (用于less编译出来的css合并成一个用的)
4.安装gulp-plumber插件：npm install gulp-plumber (用于处理管道崩溃问题)
5.安装gulp-less插件：npm install gulp-notify (显示报错信息，且不终止当前gulp任务)
6.--flat 把这个文件放进了src/app中，而不是单独的目录中
7.--module=app告诉CLI把它注册到AppModule的imports数组中。
```
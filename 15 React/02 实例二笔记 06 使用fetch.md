 ### 介绍
 fetch是一种可代替ajax获取/提交数据的技术，有些高级浏览器可以`window.fetch`使用了。相比jQuery.ajax更轻量，而且它原生支持promise，更加符合现在的编程习惯。
 
 ### 安装
 ```
 npm install whatwg-fetch --save 
 
 // 为了兼容老版本浏览器，可安装如下
 npm install es6-promise --save
 ```
 
 ### 基本使用
 ```
 import 'whatwg-fetch'
 import 'es6-promise'
 
 // get请求，第一个参数：url；第二个参数：配置信息。
 export function getData() {
    // '/api/1'获取字符串
    var result = fetch('/api/1', {
        credentials: 'include',
        headers: {
            'Accept': 'application/json, text/plain, */*'
        }
     })
     
     result.then(res => {
         return res.text()
     }).then(text => {
         console.log(text)
     })
     
     // '/api/2' 获取json
     var result1 = fetch('/api/2', {
         credentials: 'include',
         headers: {
            'Accept': 'application/json, text/plain, */*'
         }
     })
     
     result1.then(res => {
         return res.json()
     }).then(json => {
         console.log(json)
     })
 }
 
 
 // post请求
 export function postData() {
     // '/api/post' 提交数据
     var result = fetch('/api/post', {
         method: 'post',
         credentials: 'include',
         headers: {
             'Accept': 'application/json, text/plain, */*',
             'Content-Type': 'application/x-www-form-urlencoded'
         }
         // 注意post时候参数的形式
         body: 'a=100&b=200'
     })
     
     result.then(res => {
         return res.json()
     }).then(json => {
         console.log(json)
     })
 }
 ```
 
 ### 数据模拟Mock
 - 模拟静态数据：按既定的数据格式，自己提供一些静态的JSON数据，用相关工具(fis3)做接口来获取这些数据。
 - 模拟动态接口：即自己用一个web框架，按照既定的接口和数据结构的要求，自己模拟后端接口的功能，让前端项目能顺利跑起来。该方式适用于新开发的项目，前后端同时开发。
 - 转发线上接口：项目开发中，所有的接口直接用代理获取线上数据，post的数据也直接提交到线上。该方法适合成熟项目中。
 
### 安装koa（适用于后端）
```
npm install koa koa-body koa-router --save-dev
```
- 模拟接口的代码都写在`./mock`目录下。
- 执行`npm run mock`即可启动模拟的接口服务。
- 使用webpack-dev-server代理
需要`webpack-dev-server`做一个代理的转发.配置代码在`./webpack.config.js`中.
```
devServer: {
    proxy: {
        // 凡是'/api'开头的http请求,都会被代理到localhost:3000上,由koa提供mock数据.
        // koa代码在./mock目录中,启动命令为npm run mock
        '/api': {
            target: 'http://localhost:3000',
            secure: false
        }
    }
}
```
```
[server.js]
devServer: {
    proxy: {
        // 凡是'/api'开头的http请求,都会被代理到localhost:3000
        // koa代码在./mock目录中,启动命令为npm run mock
        '/api': {
            target: 'http://localhost:3000',
            secure: false
        }
    },
    contentBase: './public', //本地服务起所加载的页面所在的目录
    colors: true, // 终端中输出结果为彩色
    historyApiFallbak: true, // 不跳转
    inline: true, // 实时刷新
    hot: true // 使用热加载插件 HotModuleReplacementPlugin
}
```
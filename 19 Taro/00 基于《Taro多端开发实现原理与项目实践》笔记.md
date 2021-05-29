[本文链接](https://juejin.im/book/6844733744830480397/section/6844733744910336014)
******
## 1. React相关知识
#### 1.1 proos与state
props与state是React组件中最重要的两个状态
- props：父组件传给子组件的数据，挂载在子组件的`this.props`上
```
// 子组件
class Welcome extends React.Component {
    render() {
        return <h1>Hello,{this.props.name}</h1>
    }
}
// 父组件
class Demo extends React.Component {
    render() {
        return <Welcome name='aotu,taro!' />
    }
}
//最终页面渲染出
<h1>Hello,aotu,taro!</h1>
```
- state:属于组件自己内部的数据状态，一般在`constructor`构造函数里初始化定义state。
```
class Welcome extends React.Component {
    constructor(props) {
        super(props);
        this.state = {name: 'aotu,taro!'}
    }
    render() {
        return <h1>Hello,{this.state.name}</h1>
    }
}
// 使用this.setState更改值
this.setState({name: 'hey!hey!hey!'})
```
#### 1.2 组件的生命周期
指的是一个React组件从挂载，更新，销毁过程中会执行的生命狗子函数。
```
class Clock extends React.Component {
    constructor(props) { // 组件的构造函数，一般回在这里进行`state`的初始化，事件的绑定等。
        super(props);
        this.state = {date: new Date()}
    }
}
render() {
    return (
        <div>
            <h1>Hello,world</h1>
            <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
        </div>
    )
}
```
- 
## 2.小程序相关知识
#### 2.1 生命周期
- 应用的生命周期
    + onLaunch:当小程序初始化完成时，会出发onLaunch，且全局只触发一次
    + onShow:当小程序启动，或从后台进入前台显示，会触发onShow
    + onHide:当小程序从前台进入后台，会触发onHide
- 页面的生命周期
    + onLoad:监听页面加载的函数
    + onReady:监听页面初次渲染完成的函数
    + onShow:监听页面显示的函数
    + onHide:监听页面隐藏的函数
    + onUnload:监听页面卸载的函数

#### 2.2 流行的小程序开发框架
- WePY：较早的小程序开发框架。是腾讯内部开源的一款框架。主要解决了小程序开发较为松散，不能用 NPM 包，自定义组件开发不友好等问题。相比于原生的开发方式，已经是大大地增强了开发体验，提高了开发效率。
- mpvue：美团点评技术团队开源的一款小程序开发框架。相比较WePY，mpvue则是完全用vue的开发方式来开发小程序，开发体验较WePY相比有一定的提升。
- Taro：京东开源的一款小程序开发框架，与mpvue相反。Taro用的是React的开发方式来开发小程序的。

#### 2.3 Taro的安装与使用
Taro是基于NodeJS的多端统一开发框架。安装好npm或者yarn后，就可以全局安装Taro开发工具了。
```
// npm安装
npm install -g @tarojs/cli
// yarn安装
yarn global add @tarojs/cli

// 创建模板项目
taro init myApp

// 更新Taro三种方式
taro update self
npm i -g @tarojs/cli@latest
yarn global add @tarojs/cli@latest

// 更新项目中Taro相关的依赖，需要在项目下执行
taro update project
```

## 3.Taro开发说明与注意事项
#### 3.1 微信小程序开发工具的配置
-  设置关闭ES6转ES5功能
-  设置关闭上传代码时样式自动补全
-  设置关闭代码压缩上传

#### 3.2 Taro（针对v1.1）与React的差异
- 暂不支持在render()之外的方法定义jsx。由于微信小程序的template不能动态传值和传入函数，Taro暂时也没有办法支持在类方法中定义JSX。
- 不能再包含JSX元素的map循环中使用if表达式，尽量在map循环中使用条件表达式或逻辑表达式。
- 不能使用Array.map之外的方法操作JSX数组。只能是先处理好需要遍历的数组，然后再用处理好的数组调用map方法。
- 不能在JSX参数中使用匿名函数，需要使用bind或类参数绑定函数。
- 不能在JSX参数中使用对象展开符。只能是开发者自行赋值。
- 不允许在JSX参数（props）中传入JSX元素。只能通过props传值在JSX模板中预先判定显示内容，或通过props.children来嵌套子组件。
- 不支持无状态组件。只能使用class定义组件。

#### 3.3 命名规范
    + 使用驼峰命名法`onClick`
    + 方法名不能含有数字
    + 方法名不能以下划线开头或结尾
    + 方法名的长度不能大于20

#### 3.4 推荐安装ESLint编辑器插件
通过ESLint来获得人性化的提示

#### 3.5 最佳编码方式
- 组件样式说明：微信小程序的自定义组件样式默认是不受外部样式影响的。
- 给组件设置`defaultProps`:组件设置的`defaultProps`回在运行时用来弥补编译时处理不到的情况，里面所有的属性都会被设置到`properties`中初始化组件，正确设置`defaultProps`可以避免很多异常情况的出现。
- 组件传递函数属性名以`on`开头：在Taro中，父组件要往子组件传递函数，属性名必须以`on`开头。
```
// 当自定义组件触发"myevent"事件时，请用"onMyEvent"方法
<component-tag-name bindmyevent="onMyEvent" />
```
- 小程序端不要再组件中打印传入的函数
- 小程序端不要将在模板中用到的数据设置为`undefined`
- 小程序端不要在组件中打印`this.props.children`
- 组件属性传递注意不要以`id`、`class`、`style`作为自定义组件的属性与内部state的名称，因为这些属性名在微信小程序中会丢失。
- 不要在`state`与`props`上用同名的字段，因为这些字段在微信小程序中都会挂在`data上`
- 小程序页面生命周期`componentWillMount`不一致问题。
- JS编码必须用单引号
- 不要以解构的方式来通过`env`配置`process.env`环境变量，而是直接用完整书写的方式来使用`process.env.NODE_ENV`
- 预加载：在微信小程序中，从调用 Taro.navigateTo、Taro.redirectTo 或 Taro.switchTab 后，到页面触发 componentWillMount 会有一定延时。因此一些网络请求可以提前到发起跳转前一刻去请求。Taro 提供了 componentWillPreload 钩子，它接收页面跳转的参数作为参数。可以把需要预加载的内容通过 return 返回，然后在页面触发 componentWillMount 后即可通过 this.$preloadData 获取到预加载的内容。

## CLI原理及不同端的运行机制
taro-cli负责Taro脚手架初始化和项目构建的命令行工具，NPM包的链接在：`@tarojs/cli`,通过`npm install -g @tarojs/cli`安装。
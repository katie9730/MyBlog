## 1. 导学
### 1.1 课程概述
- React全家桶
    + React基础知识、生命周期
    + Router 4.0 语法讲解
    + Redux集成开发
- AntD UI组件
    + 最实用基础组件
    + AntD栅格系统
    + ETable组件封装
    + BaseForm组件封装
    + 表格内嵌单选、复选封装
- 公共机制封装
    + Axios请求插件封装
    + API封装
    + 错误拦截
    + 权限、菜单封装
    + 日期、金额、手机号封装
    + Loading、分页、Mock...

### 1.2 项目整体架构（3层）
- 核心库（React 16、Router 4.0、Redux）
- 中间件（Axios、Map、ECharts、AntD）
- 基本功能模块（菜单、权限、Header、Footer、ETable、EForm、Loading、API、Axios）

## 2. React介绍
### 2.1 React基本介绍
- Facebook开源的一个JavaScript库
- React结合生态库构成一个MV*框架(只关注视图View+数据层Model)
- 生态介绍
    + Vue生态：Vue + Vue-Router + Vuex + Axios + Babel + Webpack
    + React生态：React + React-Router + Redux + Axios + Babel + webpack
- React特点 
    + 声明式编码:只需要声明在哪里(where)做什么(what),而无需关心如何实现(how) 
        * [补充]编程式编码：需要以具体代码表达在哪里(where)做什么(what),如何实现(how)
    + 组件化编码:
    + 高效-高效的DOM Diff算法，最小化页面重绘
    + 单向数据流


### 2.2 React脚手架、Yarn介绍
- 如何安装及使用React脚手架
```
// 安装
npm install -g create-react-app
create-react-app my-app
// 使用
cd my-app
npm start

// 查看版本
create-react-app --version
```
- 什么是Yarn，为什么要使用Yarn
    + Yarn是新一代包管理工具
    + 速度快
    + 安装版本统一、更安全
    + 更简洁的输出
    + 更好的语义化
- 如何使用Yarn
```
yarn init   // 初始化项目
yarn add    // 安装包
yarn remove // 删除包
yarn / yarn install // 安装依赖
```
### 2.3 React生命周期介绍
- getDefaultProps：初始化Props属性，props则来着父组件或其他组件。
- getInitialState: 初始化当前组件的状态。
- componentWillMount: 组件加载之前调用。
- render：在getInitialState之后调用，UI获得渲染。
- componentDidMount: DOM渲染完之后调用。
- componentWillReceiveProps: 组件传递调用的方法。
- shouldComponentUpdate: 组件的更新。
- componentWillUpdate: 组件更新之前调用。
- componentDidUpdate: 组件更新之后调用。
- componentWillUnmount: 组件的销毁。

### 2.4 React生命周期顺序
- Initial render -> constructor() -> componentWillMount() -> render() -> componentDidMount() -> componentWillUnmount()
- 父组件render -> componentWillReceiveProps() -> shouldComponentUpdate()`this.setState()` -> componentWillUpdate()`this.forceUpdate()` -> render() -> componentDidUpdate() -> componentWillUnmount()

## 3. 主页面架构设计
### 3.1 基础插件安装，less文件加载配置
#### 基础插件安装
- 安装React-Router、Axios
`yarn add react-router-dom axios`
- 安装AntD
`yarn add antd`
- 暴露webpack配置文件
`yarn eject`
- 安装less-loader，并修改less-loader（https://blog.csdn.net/Pinkr28/article/details/106923888）
`yarn add less-loader less`
- 按需加载配置
`yarn add babel-plugin-import --dev`



### 3.2 项目主页结构开发
- 主页结构定义
    + 页面结构定义
    + 目录结构定义
    + 栅格系统使用
    + calc计算方法使用

### 3.3 菜单组件开发

### 3.4 头部组件开发

### 3.5 底部组件开发
- 底部组件布局
- Home页面实现
- 使用css实现箭头图标

## 4. React Router 4.0
### 4.1 React Router 4.0 基本概念介绍
#### react-router和react-router-dom理解
- 4.0版本已不需要路由配置，一切皆组件
- react-router：提供了一些router的核心api，包括Router，Route，Switch等
- react-router-dom：提供了BrowserRouter, HashRouter, Route, Link, NavLink

#### 路由模块安装
- npm install react-router-dom --save
- yarn add react-router-dom

#### react-router-dom核心用法
- HashRouter和BrowserRouter
- Route: path, exact:精确匹配, component, render
- NavLink, Link
- Switch：一旦匹配到路由就不会再往下进行匹配了
- Redirect

#### HashRouter和BrowserRouter
- HashRouter写法：http://localhost:3000/#/admin/buttons
- BrowserRouter写法: http://localhost:3000/admin/buttons

#### Route用法
```
// 写法一
<Route path="/admin/ui/buttons" component={Buttons} />

// 写法二
<Route path="/admin" render={() => 
    <Admin>
        <Route path="/admin/home" component={Home} />
    </Admin>
} />
```

#### Link用法
```
// 写法一
import { Link } from 'react-router-dom'
const Header = () => {
    <header>
        <nav>
            <ul>
                <li><Link to='/'>Home</Link></li>
                <li><Link to='/about'>about</li>
                <li><Link to='three'>three</Link></li>
            </ul>
        </nav>
    </header>
}

// 写法二
<Link to={{ pathname: '/three/7' }}> Three #7 </Link>
// 写法二解析
<Route path="/three/:number" /> 取值：this.props.match.params.number
```

#### Switch用法
```
<Switch>
    <Route path="/admin/ui/buttons" component={Buttons} />
    <Route path="/admin/ui/modals" component={Modals} />
    <Route path="/admin/ui/loading" component={Loading} />
    <Route path="/admin/ui/notification" component={Notification} />
    <Route path="/admin/ui/messages" component={Messages} />
    <Route path="/admin/ui/tabs" component={Tabs} />
    <Route path="/admin/ui/gallery" component={Gallery} />
    <Route path="/admin/ui/carousel" component={Carousel} />
</Switch>
```

#### Redirect
- 路由重定向：`<Redirect to="/admin/home" />`
 
### 4.2 React Router 4.0 Demo介绍
- 基本路由功能Demo实现-混合组件化（Link、HashRouter、Route）
- 基本路由功能Demo实现-配置化（Link、HashRouter、Route）
```
<Route exact={true}  path="/" component={Main}></Route> // exact={true} 用来做精准匹配
```


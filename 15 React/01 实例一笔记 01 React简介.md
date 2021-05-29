#### React
- React是一个用于创建可复用，可聚合的web组件的js库。它只提供了前端MVC框架中的“v”层，并不是一个完整的前端MVXC框架。一个React的组件可以理解成一个独立的函数，它可以接受参数(props)，可复用，可以传递，返回结果(渲染组件)。React特性有如下
    + 组件化：而不是写一大堆HTML模板，js逻辑与HTML标签紧密相连并且极易理解。
    + 单向数据流：数据一旦更新，就直接重新渲染整个app。就是让React如此牛逼的关键点。
    + 虚拟DOM树：js虽快，但操作dom的时候就很慢，React的处理方式如下
        * React重建DOM树
        * 找到与上个版本的DOM的差异
        * 计算出最新的DOM更新操作
        * 从操作队列中批量地执行DOM更新操作
- React可以在Node.js(服务端)中运行
    + 服务端与客户端共用逻辑
    + SEO友好，便于生成缓存的单页应用
    + 直接渲染特定的页面，不用渲染整个app

- 如何管理UI的状态
    + 修改DOM树
    + 修改数据
    + 接受用户的输入
    + 异步API数据请求
- 传统服务器与React渲染比较
    + 传统方式
        * 浏览器请求页面
        * 服务器请求数据库
        * 将数据传给模板
        * 模板渲染页面
    + React的渲染方式
        * 用户输入
        * 从API获取数据
        * 将数据传给顶层组件
        * React将每个组件渲染出来

- 简单的React实例
```
// 第一步：组件定义
var HelloWorld = React.createClass({
    render: function() {
        return <p>Hello {this.props.name}</p>
    }
})
// 第二步：渲染组件
React.render(
    <HelloWorld name="John" />
    document.getElementById("app")
)

```

#### 学习React之前必须掌握的JavaScript基础知识
- 判断this的指向
- class(类)
- ES6语法规范
- npm包管理器
- 原型、原型链
- 数组常用方法
- 模块化

#### 相关js库
- react.js: React核心库
- react-dom.js: 提供操作DOM的react扩展库
- babel.min.js: 解析JSX语法代码转为JS代码的库

#### JSX
- jsx是javaScript的XML语法扩展。
- React没有人为的将标记与逻辑进行分离到不同文件中，而是通过将两者共同存放在称之为“组件”的松散耦合单元之中，来实现关注点分离。

#### React是如何使用JSX的
```
// 此为JSX
<p className="hello">
    Hello {this.props.name}
</p>
// JSX编译成React的语法
React.createElement("p", {className: "hello"},
    "Hello", this.props.name
)
```
## 1. ReactJS简介
+ React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram 的网站。做出来以后，发现这套东西很好用，**就在2013年5月开源了**。
+ 由于 React 的设计思想极其独特，属于革命性创新，性能出众，代码逻辑却非常简单。所以，越来越多的人开始关注和使用，认为它可能是将来 Web 开发的主流工具。
+ library
+ Framework


## 2. 前端三大主流框架
+ Angular.js：出来最早的前端框架，学习曲线比较陡，NG1学起来比较麻烦，NG2开始，进行了一系列的改革，也开始启用组件化了；在NG中，也支持使用TS（TypeScript）进行编程；
+ Vue.js：最火的一门前端框架，它是中国人开发的，对我我们来说，文档要友好一些；
+ React.js：最流行的一门框架，因为它的设计很优秀；
+ windowsPhone 7    7.5   8   10


## 3. React与vue.js的对比
#### 3.1 组件化方面
1. 什么是模块化：从 **代码** 的角度，去分析问题，把我们编程时候的业务逻辑，分割到不同的模块中来进行开发，这样能够**方便代码的重用**；
2. 什么是组件化：从 **UI** 的角度，去分析问题，把一个页面，拆分为一些互不相干的小组件，随着我们项目的开发，我们手里的组件会越来越多，最后，我们如果要实现一个页面，可能直接把现有的组件拿过来进行拼接，就能快速得到一个完整的页面， 这样方**便了UI元素的重用**；**组件是元素的集合体**；
3. 组件化的好处：
4. Vue是如何实现组件化的：.vue 组件模板文件，浏览器不识别这样的.vue文件，所以，在运行前，会把 .vue 预先编译成真正的组件；
 + template： UI结构
 + script： 业务逻辑和数据
 + style： UI的样式
5. React如何实现组件化：在React中实现组件化的时候，根本没有 像 .vue 这样的模板文件，而是，直接使用JS代码的形式，去创建任何你想要的组件；
 + React中的组件，都是直接在 js 文件中定义的；
 + React的组件，并没有把一个组件 拆分为 三部分（结构、样式、业务逻辑），而是全部使用JS来实现一个组件的；（也就是说：结构、样式、业务逻辑是混合在JS里面一起编写出来的）

#### 3.2 开发团队方面
+ React是由FaceBook前端官方团队进行维护和更新的；因此，React的维护开发团队，技术实力比较雄厚；
+ Vue：第一版，主要是有作者 尤雨溪 专门进行维护的，当 Vue更新到 2.x 版本后，也有了一个小团队进行相关的维护和开发；

#### 3.3 社区方面
+ 在社区方面，React由于诞生的较早，所以社区比较强大，一些常见的问题、坑、最优解决方案，文档、博客在社区中都是可以很方便就能找到的；
+ Vue是近两年才诞生开源出来的，所以，它的社区相对于React来说，要小巧一些，所以，可能有的一些坑，没人踩过；

#### 3.4 移动APP开发体验方面
+ Vue，结合 Weex 这门技术，提供了 迁移到 移动端App开发的体验（Weex，目前只是一个 小的玩具， 并没有很成功的 大案例；）
+ React，结合 ReactNative，也提供了无缝迁移到 移动App的开发体验（RN用的最多，也是最火最流行的）；

## 4.React中几个核心的概念
#### 4.1 虚拟DOM（Virtual Document Object Model）
- DOM的本质是什么：就是用JS表示的UI元素
- DOM和虚拟DOM的区别：
    + DOM是由浏览器中的JS提供的功能，所以我们只能认为的使用浏览器提供的固定的API来操作DOM对象
    + 虚拟DOM：并不是由浏览器提供的，而是我们程序员手动模拟实现的，类似于浏览器中的DOM，但是有着本质的区别
- 为什么要实现虚拟DOM：使用JS对象来模拟DOM树
- 什么是React中的虚拟DOM
- 虚拟DOM的目的：为了实现DOM节点的高效更新

#### 4.2 Diff算法
- tree diff:新旧DOM树，逐层对比的方式，就叫做tree diff，每当我们从前到后，把所有层的节点对比完成后，必然能够找到那些需要被更新的元素。
- component diff:组件之间的对比。如果两个组件的类型相同，则表示不需要更新，若类型不同，则立即移除旧组件，将新组建替换上去
- element diff:元素之间的对比。
- key：该属性是将页面上的DOM节点和虚拟DOM中的对象，做一层关联。

## 5. React项目的创建
1. 运行npm i react react-dom -S 安装包
2. 导入两个相关的包
```
// react，专门用来创建React组件、组件生命周期等
import React from 'react'  
// react-dom, 主要封装了和DOM操作相关的包，比如把组件渲染到页面上
import ReactDOM from 'react-dom'
```
3. 使用JS创建虚拟DOM节点
```
// 在react中，如果要创建DOM元素了，只能使用React提供的JS API来创建，不能直接像vue中那样，手写HTML元素
// React.createElement('元素类型','属性对象：该元素上有哪些属性','当前元素的子节点')方法，用于创建虚拟DOM对象。

<div title="this is a div" id="mydiv">这是一个div</div>
var myH1 = React.createElement('h1',null,'这是一个大大的H1')
var myDiv = React.createElement('div',{ title:'this is a div', id:"mydiv" }, '这是一个div', myH1)
```
4. 使用ReactDOM把元素渲染到页面指定的容器中
```
// ReactDOM.render('要渲染的虚拟DOM元素','要渲染到页面上的哪个位置中')。其中第二个参数，需要传递一个原生的DOM对象。与vue不同，不接受“#app”这样的字符串
ReactDOM.render(myDiv, document.getElementById('app'))
```
## 6. JSX语法
1. **使用JSX语法：** npm i babel-preset-react -d,然后在.babelrc中添加语法配置
2. **JSX语法本质：** 使用React.createElement形式创建虚拟DOM来实现，而不是直接将HTML渲染到页面上
3. **书写规范**
    + JS写到{}内部
    + 注释写到{}内部
4. **编译引擎**
    + 当遇到`<`时当作HTML代码去编译
    + 当遇到`{}`时当作JS代码去编译
5. JSX中，class属性应写成className，for属性应写成htmlFor
6. 当JSX创建DOM时，所有节点都必须有唯一的根元素来包裹

## 6. React中创建组件的方式，两者的本质区别在于有无state属性
- 使用构造函数创建组件，也称“无状态组件”
    + 父组件向子组件传递数据
    + 属性扩散
    + 将组件封装到单独的文件中
- 使用class关键字创建组件，也称“有状态组件”
    + 了解ES6中class关键字的使用,基于class关键字创建组件
    ```
    class Person extends React.Component{
        //在class创建的组建中，必须定义一个render函数
        render(){
            //在render函数中，必须返回一个null或者符合规范的虚拟DOM元素
            return <div>
                <h1>这是用class关键字创建的组件！</h1>
            </div>;
        }
    }
    ```

## 7. 手动创建基本的webpack4.x项目
- 6.1 运行`npm init -y`快速初始化项目
- 6.2 在项目根目录创建`src`源代码目录和`dist`产品目录
- 6.3 在src目录下创建`index.html`
- 6.4 使用cnpm安装webpack，运行`cnpm i webpack webpack-cli -d`
    + 全局运行`npm i cnpm -g`
- 6.5 注意：webpack 4.x提供了约定大于配置的概念；目的是为了尽量减少配置文件的体积；
    + 默认约定了：
    + 打包的入口是`src`->`index.js`
    + 打包的输出文件是`dist`->`main.js`

## 相关文章
- [React数据流和组件间的沟通总结](http://www.cnblogs.com/tim100/p/6050514.html)
- [单向数据流和双向绑定各有什么优缺点？](https://segmentfault.com/q/1010000005876655/a-1020000005876751)
- [怎么更好的理解虚拟DOM?](https://www.zhihu.com/question/29504639?sort=created)
- [React中文文档 - 版本较低](http://www.css88.com/react/index.html)
- [React 源码剖析系列 － 不可思议的 react diff](http://blog.csdn.net/yczz/article/details/49886061)
- [深入浅出React（四）：虚拟DOM Diff算法解析](http://www.infoq.com/cn/articles/react-dom-diff?from=timeline&isappinstalled=0)
- [一看就懂的ReactJs入门教程（精华版）](http://www.cocoachina.com/webapp/20150721/12692.html)
- [CSS Modules 用法教程](http://www.ruanyifeng.com/blog/2016/06/css_modules.html)
- [将MarkDown转换为HTML页面](http://blog.csdn.net/itzhongzi/article/details/66045880)
- [win7命令行 端口占用 查询进程号 杀进程](https://jingyan.baidu.com/article/0320e2c1c9cf0e1b87507b26.html)

## 完结 2019/10/11
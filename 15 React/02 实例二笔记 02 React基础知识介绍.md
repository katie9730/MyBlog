#### 创建React项目
- 使用npx创建项目
```
npx create-react-app my-app
cd my-app
npm run start
```
- 使用npm创建项目
```
npm install -g create-react-app // 全局安装create-react-app
create-react-app my-app // 创建my-app项目
```
> 引自：https://www.jianshu.com/p/68e849768d8e

#### hello world
```
import React from 'react'
import { render } from 'react-dom'
// 定义组件
class Hello extends React.Component {
    render() {
        // return里面写jsx语法
        return (
            <p>hello world</p>
        )
    }
}

// 渲染组件到页面
render(
    <Hello />,
    document.getElementById('root')
)
```

#### jsx语法
React里面写模板要使用jsx语法，它其实和html相似但是又有些不同。以下简述jsx特点。
- 使用一个父节点包裹：jsx中不能一次性返回零散的多个节点，如果有则需要包含在一个父节点中。
```
var m = 100
return ( // return里面写jsx语法
    <div>
        <p>段落1</p>
        <p>{m ? '100': 'not 100'}</p> // 大括号中可以放变量，三元表达式，函数等
        <p>段落3</p>
    </div>
)
```
- 事件：拿click事件为例，要在标签上绑定click事件
```
class Hello extends React.Component {
    render() {
        var arr = ['aa', 'bb', 'cc']
        return (
            <p onClick={this.clickHandler.bind(this)}>hello world</p>
            <p style={{fontSize: '50px', display: 'block'}}>345</p>
            <ul>
                {arr.map(function(item, index){
                    return <li>{item}</li>
                })}
            </ul>
        )
    }
    clickHandler(e) {
        // e即js中的事件对象，例如e.preventDefault()
        // 函数执行时this即组件本身，因为上面的.bind(this)
        console.log(Date.now())
    }
}
// 注意,`onClick`是驼峰式写法，以及`.bind(this)`的作用
```

- 数据传递&数据变化
    + props：React中，props是作为父组件给子组件传递数据使用的。并且props不能被自身修改。
    ```
    render() {
        return (
            <p>{this.props.title}</p>
        )
    }
    ```
    + props && state:state是用于组件内部自身属性发生的变化。
    ```
    class Hello extends React.Conponent {
        constructor(props, context) {
            super(props, context);
            this.state = {
                // 显示当前时间
                now: Date.now()
            }
        }
        render() {
            return (
                <div>
                    <p onClick={this.clickHandler.bind(this)}>hello world {this.state.now}</p>
                </div>
            )
        }
        clickHandler() {
            // 设置state的值的时候，一定要用this.setState，不能直接赋值修改
            this.setState({
                this.setState({
                    now:Date.now()
                })
            })
        }
    }
    ```
    
- 智能组件 && 木偶组件
    + 智能组件`./app/containers`：又称页面。只对数据负责，只需要获取数据、定义好数据操作的相关函数，然后将数据、函数直接传递给具体实现的组件。
    + 木偶组件`./app/components`：从智能组件那里接受到数据、函数、然后就开始做一些展示工作。它的工作就是把拿到的数据展示给用户。

- 生命周期
    + getInitialState:初始化组件state数据，但在es6语法中，可用以下方式代替
    ```
    class Hello extends React.Component {
        constructor(props, context) {
            super(props, context)
            // 初始化组件state数据
            this.state = {
                now: Date.now()
            }
        }
    }
    ```
    + render:最常用的hook，返回组件要渲染的模板。
    
    + componentDidMount:组件第一次加载时渲染完成的事件，一般在此获取网络数据。实际开始项目开发时，会经常用到。
    + shouldComponentUpdate:主要用于性能优化。
    + componentDidUpdate:组件更新之后触发的事件，一般用于清空并更新数据。
    + componentWillUnmount：组件在销毁之前触发的事件，一般用户存储一些特殊信息，以及清理setTimeout事件等。
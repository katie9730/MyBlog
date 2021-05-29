#### 安装
`npm install react-router --save`,完成后可查看`package.json`的变化。
> 注意这里得`hashHistory`,规定用url中的hash来表示router例如`localhost:8080/#/list`。与之对应的还有一个`browserHistory`也可用，它就不适用hash，直接可以这样`localhost:8080/list`表示。但是后者需要服务器支持，我们这里用前者。两者在前端开发中，只用起来都是一样的，只是表示形式不一样。

#### 使用router
`./app/index.jsx`中的代码如下，这样就使用了我们刚才定义的routeMap组件。
```
import React from 'react'
import { render } from 'react-dom'
import { hashHistory } from 'react-router'
import RouteMap from './router/routeMap'

render(
    <RouteMap history={hashHistory}/>,
    document.getElementById('root')
)
```
注意这里的`hashHistory`,规定用url中的hash来表示router，例如`localhost:8080/#/list`。与之对应的还有一个`browserHistory`也可用，它就不使用hash，直接可以这样`localhost:8080/list`表示。但是后者需要服务器端支持，我们这里用前者。两者再前端开发中，使用起来都是一样的，只是表示形式不一样。

#### 两种路由跳转方式
- html方式： `<Link to="/list">to list</Link>`
- js方式
```
class List extends React.Component {
    render() {
        const arr = [1, 2, 3]
        return (
            <ul>
                {arr.map((item, index) =>{
                    return <li key={index} onClick={this.clickHandler.bind(this, item)}>js jump</li>
                })}
            </ul>
        )
    }
    clickHandler(value) {
        hashHistory.push('/detail/' + value)
    }
}
```

#### router参数
```
<Route path="detail/:id/:type" component={Detail} />
// 获取
{ this.props.params.id },{ this.props.params.type }
```

#### 懒加载
针对大型项目的静态资源懒加载，react-router提供了`huge-apps`，它将react-router本身和webpack的`require.ensure`结合起来来解决这个问题。
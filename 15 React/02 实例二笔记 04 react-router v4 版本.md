### 1. 开场白
React用于在客户端渲染创建单页应用(SPA)。它可以实现视图跳转是不导致整个页面被重新加载。以下是SPA特性
- 应用中每个视图都对应唯一URL来区分视图。
- 浏览器的前进后退按钮应该正常工作。
- 动态生成的嵌套视图也对应url。

#### 1.1 路由跳转
指在同步保持浏览器URL的过程中渲染页面中的视图。React Router以声明式的操作路由跳转。声明式路由方法允许你控制应用中的数据流。`<Route path='/about' component={About} />`

### 2. 安装React Router
```
npm install --save react-router-dom
```
React Router库包含以下三个包
- react-router: 路由核心包。
- react-router-dom: 用于开发网站。
- react-router-native: 用于移动应用的开发环境使用React Native。

### 3. React Router基础
```
<Router>
    <Route exact path="/" component={home} />
    <Route path="/category" component={Category} />
    <Route path="/login" component={Login} />
    <Route path="/products" component={Products} />
</Router>
```
### 4. Router
基于浏览器应用路由类型分为两种`<BrowserRouter>`和`<HashRouter>`
- <BrowserRouter>: 使用了HTML5的history API来记录路由历史。http://example.com/about
- <HashRouter>: 使用URL（window.location.hash）的hash部分来记录。http://example.com/#/about

#### 4.1 index.js
```
import React from 'react'
import ReactDOM from 'react-dom'

import App from './App'
import { BrowserRouter } from 'react-router-dom'

ReactDOM.render(
    <BrowserRouter>
        <App />
    </BrowserRouter>
    , document.getElementById('root')
)

```
#### 4.2 history
每个router组件创建一个history对象，用来记录当前路径`history.location`。上一步路径也存储在堆栈中。history对象有`history.push()`和`history.replace()`来实现。点击`<Link>`触发`history.push()`,点击`<Redirect>`触发`history.replace()`。

#### 4.3 Links and Routes
`<Route>`是React Router的重要组件。若当前路径匹配route的路径 ，它会渲染对应的UI。
`<Link>`用来跳转至具体的URL，并且视图重新渲染不会导致浏览器刷新。

### 5. Demo合集
#### 5.1 Demo1:基础路由
```
[src/App.js]
import React, { Component } from 'react'
import { Link, Route, Switch } from 'react-router-dom'

/*Home component*/
const Home = () => {
    <div>
        <h2>Home</h2>
    </div>
}

/*Category component*/
const Category = () => {
    <div>
        <h2>Category</h2>
    </div>
}

/*Products component*/
const Products = () => {
    <div>
        <h2>Products</h2>
    </div>
}

/*App component*/
class App extends React.Component {
    render() {
        return (
            <div>
                <nav className="navbar navbar-light">
                    <ul className="nav navbar-nav">
                        <li><Link to="/">Homes</Link></li>
                        <li><Link to="/category">category</Link></li>
                        <li><Link to="/products">products</Link></li>
                    </ul>
                </nav>
                
                <Route path="/" component={Home} />
                <Route path="/category" component={Category} />
                <Route path="/products" component={Products} />
            </div>
        )
    }
}
```
在App组件中，`Route`的路径与当前路径匹配，对应组件就会被渲染。对应渲染的组件传给了第二个prop--component。若想要路由在路径完全相同时渲染，可以使用`exact={true}`props。

##### 5.1.1 嵌套路由
`<Route>`有三个可以用来定义渲染内容的props
- component：当url匹配时，router将会传递组件使用`React.createElement`来生成一个React元素。
- render：适合行内渲染，在当前路径匹配路由路径时，render prop期望一个函数返回一个元素。
- children：期望一个函数返回一个React元素。然而，不管路径是否匹配，children都会被渲染。

##### 5.1.2 Path and match
- path:用来表示路由匹配的URL部分。React Router使用了Path-to-RegExp库将路径字符串转为正则表达式。然后正则表达式会匹配当前路径。
- match：路由路径和当前路径成功匹配，会生成一个对象。match对象有更多关与URL和path的信息。这些信息可以通过他的属性获取
    + `match.url`:返回URL匹配部分的字符串。对于创建嵌套的<Link>有用。
    + `match.path`:返回路由路径字符串`<Route path="">`。用来创建嵌套的`<Route>`。
    + `match.isExact`:返回布尔值，准确则返回true。
    + `match.params`:返回一个对象包含Path-to-RegExp包从URL解析的键值对。

##### 5.1.3 switch组件
当URL为`/products`,所有匹配`/products`路径的route都会被渲染。所以，那个path为`:id`的`<Route>`会跟着Products组件一块渲染。有`<switch>`组件的话，只有第一个匹配路径的子`<Route>`会渲染。

#### 5.2 Demo2:嵌套路由
```
[src/App.js]
import React, { Component } from 'react'
import { Link, Route, Switch } from 'react-router-dom'
import Category from './Category'

class App extends Component {
    render() {
        return (
            <div>
                <nav className="navbar navbar-light">
                  <ul className="nav navbar-nav">
                    <li><Link to="/">Homes</Link></li>
                    <li><Link to="/category">Category</Link></li>
                    <li><Link to="/products">Products</Link></li>
                  </ul>
                </nav>
               
                <Switch>
                    <Route exact path="/" component={Home} />
                    <Route exact path="/Category" component={Category} />
                    <Route exact path="/products" component={Products} />
                </Switch>
               
            </div>
        )
    }
}

export defalut App

// 在版本4中，嵌套的<Route>最好放在父元素里面。所以Category组件就是这里的父组件，父组件中定义`category/:name`路由。
```
```
[src/Category.jsx]
import React from 'react'
import { Link, Route } from 'react-router-dom'

const Category = ({ match }) => {
    return (
        <div>
            <ul>
                <li><Link to={`$match.url/shoes`}>Shoes</Link></li>
                <li><Link to={`$match.url/boots`}>Boots</Link></li>
                <li><Link to={`$match.url/footwear`}>Footwear</Link></li>
            </ul>
            <Route path={`${match.path}/:name`} render={({match}) => (<div><h3>{ match.params.name }</h3></div>)} />
        </div>
    )
}

export default Category

// match.url用来构建嵌套链接
// match.path用来构建嵌套路由
```
#### 5.3 Demo3:带path参数的嵌套路由
```
[src/Products.jsx]
const productData = [
{
  id: 1,
  name: 'NIKE Liteforce Blue Sneakers',
  description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin molestie.',
  status: 'Available'

},
{
  id: 2,
  name: 'Stylised Flip Flops and Slippers',
  description: 'Mauris finibus, massa eu tempor volutpat, magna dolor euismod dolor.',
  status: 'Out of Stock'

},
{
  id: 3,
  name: 'ADIDAS Adispree Running Shoes',
  description: 'Maecenas condimentum porttitor auctor. Maecenas viverra fringilla felis, eu pretium.',
  status: 'Available'
},
{
  id: 4,
  name: 'ADIDAS Mid Sneakers',
  description: 'Ut hendrerit venenatis lacus, vel lacinia ipsum fermentum vel. Cras.',
  status: 'Out of Stock'
},

];

```
```
[src/Products.jsx]
const Products = ({ match }) => {
    const productsData = [
        {
            id:1,
            name: 'NIKE liteforce Blue Sneakers',
            description: 'Lorem ipsum dolor sit amet, consectetur adipiscing elit. Proin molestie.',
            status: 'Available'
        }
    ]
}

var linkList = productsData.map((product) => {
    return(
        <li>
            <Link to={`${match.url}/${product.id}`}>
                {product.name}
            </Link>
        </li>
    )
})

return (
    <div>
        <div>
         <div>
           <h3> Products</h3>
           <ul> {linkList} </ul>
         </div>
        </div>

        <Route path={`${match.url}/:productId`} render={ (props) => <Product data={productsData}> } { ...props } />
        <Route exact path={match.url} render={()=>(
            <div>Please select a product.</div>
        ) />
    </div>
)

```

### 6. 保护式路由
#### 6.1 重定向
类似服务起重定向，`<Redirect>`会将history堆栈的当前路径替换为新路径。新路径通过`to`prop传递。
```
`<Redirect to={{pathname: '/login', state: {from: props.location}}}`
```
若账户被注销，想进入`/admin`页面，则会被重定向到`/login`页面。当前路径信息则通过state传递。

#### 6.2 自定义路由
```
<Switch>
    <Route exact path="/" component={Home} data={data} />
    <Route path="/category" component={category} />
    <Route path="/login" component={Login} />
    <PrivateRoute authed={fakeAuth.isAuthenticated} path='/products' component={Product} /> // 若用户已登录fakeAuth.isAuthenticated返回true,反之亦然。这是PrivateRoute的定义。
</Switch>
```

## 完结 2020/11/9 https://www.zcfy.cc/article/react-router-v4-the-complete-guide-mdash-sitepoint-4448.html
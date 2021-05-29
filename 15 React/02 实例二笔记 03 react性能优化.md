#### 性能检测
    + 安装react性能检测工具`npm i react-addons-perf --save`,然后在`./app/index.js`中运行程序
    ```
    // 性能测试
    import Perf from 'react-addons-perf'
    if (_DEV_) {
        window.Perf = Perf
    }
    ```
        * `Perf.start()`：开始检测
        * `Perf.stop()`：停止检测
        * `Perf.printWasted()`：打印出浪费性能的组件列表。
#### 性能优化-PureRenderMixin优化
React最基本的优化方式是使用`PureRenderMixin`，npm安装`npm i react-addons-pure-render-mixin --save`,然后在组件中引用并使用。
```
import React from 'react'
import PureRenderMixin from 'react-addons-pure-render-mixin'
class List extends React.Component {
    constructor(props, context) {
        super(props, context)
        this.shouldComponentUpdate = PureRenderMixin.shouldComponentUpdate.bind(this)
    }
}
```
#### 性能优化-Immutable.js优化
React的终极优化是使用Immutable.js来处理数据，Immutable实现了js中不可变数据的概念。适用于组件中props和state的数据结构较深的情况。特点：学习成本高，易遗漏，风险高。 
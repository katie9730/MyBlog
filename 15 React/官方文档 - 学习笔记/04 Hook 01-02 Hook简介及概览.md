#### 介绍
Hook是React 16.8的新增特性。可以让你在不编写class的情况下使用state以及React特性。
```
import React, {useState} from 'react'
function Example() {
    // 声明一个新的叫做“count”的state变量
    const [count, setCount] = useState(0)
    
    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>
                click me
            </button>
        </div>
    )
}
// useState就是一个Hook，通过在函数组件里调用它来给组件添加一些内部state。
// useState会返回一对值：当前状态和一个让你更新它的函数。
// 可以在事件处理函数中或其他一些地方调用这个函数。类似于this.setState。且不会将新的state与旧的state合并。

```
声明多个state变量
```
function ExampleWithManyStates() {
    // 声明多个state变量！
    const [age, setAge] = useState(42)
    const [fruit, setFruit] = useState('banana')
    const [todos, setTodos] = useState([{ text: 'Learn Hooks' }])
}
```
#### Effect Hook
`useEffect`就是一个Effect Hook。跟class组件中的`componentDidMount`、`componentDidUpdata`和`componentWillUnmount`具有相同用途。
```
import React, { useState, useEffect } from 'react'
function Example() {
    const [count, setCount] = useState(0)
    // 相当于componentDidMount和componentDidUpdate
    useEffect(()=>{
        // 使用浏览器的API更新页面标题
        document.title = `You clicked ${count} times`;
    })
    return (
        <div>
            <p>You clicked {count} times</p>
            <button onClick={() => setCount(count + 1)}>Click me</button>
        </div>
    )
}
```

#### Hook使用规则
Hook就是JavaScript函数，使用它们会有两个额外的规则
- 只能在函数最外层调用Hook。不要在循环、条件判断或者子函数中调用。
- 只能在React的函数组件中调用Hook。不要在其他JavaScript函数中调用。

#### 自定义Hook
若想要在组件之间重用一些状态逻辑。除了高阶组件和render props，自定义Hook可以在不增加组件的情况下也达到此目的。

#### 其他Hook
除此之外，还有一些使用频率较低的但是很有用的Hook。比如`useContext`可以不使用组件嵌套就可以订阅React的Context。
```
function Example() {
    const locale = useContext(LocaleContext)
    const theme = useContext(ThemeContext)
}
```

**注意**      
React 16.8.0是第一个支持Hook的版本，升级时，需注意更新所有的package，包括ReactDOM。React Native从`0.59版本`开始支持Hook。

## 完结 2021/5/7
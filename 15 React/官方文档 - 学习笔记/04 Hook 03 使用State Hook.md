#### 等价示例
```
// Hook 写法
import React, {useState} from 'react'
function Example() {
    // 声明一个叫‘count’的state变量
    const  [count, setCount] = useState(0)
    return (
        <div>
            <p>You clickekd {count} times</p>
            <button onClick={()=> setCount(count + 1)}>
                click me
            </button>
        </div>
    )
}

// 等价的class示例
class Example extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            count: 0
        }
    }
    render() {
        return (
            <div>
                <p>You clicked {this.state.count} times</p>
                <button onClick={() => this.setState({ count: this.state.count + 1 })}>
                    click me
                </button>
            </div>
        )
    }
}
```

#### Hook和函数组件
```
// 两种写法
const Example = (props) => {
    // 可以在此处使用Hook
    return <div />
}

function Example(props) => {
    // 可以在此处使用Hook
    return <div /> 
}
```

#### Hook是什么？
- Hook是什么？
    + Hook是一个特殊的函数，它可以“钩入”React特性。例如`useState`是允许在React函数组件中添加state。
- 什么时候用Hook？
    + 当函数组件需要添加state的时候。

#### 声明State变量
在函数组件中，我们没有this，所以不能分配或读取this.state。可以只能调用Hook中的`useState`。
```
import React, {useState} from 'react'
function Example() {
    const [count, setCount] = useState(0)
}
```
- 调用useState方法做了什么? ————它与class里面的this.state提供的功能完全相同。而函数退出后变量会消失，而state中的变量会被React保留.

- useState需要那些参数? ———— useState()方法里面唯一的参数就是初始state。class中通过对象对state进行初始化，而函数组件中，需要几个变量就需要调用几次useState()。

- useState方法的返回值是什么? ———— 返回值为：当前state以及更新state的函数。`const [count, setCount] = useState()`等价于`this.state.count 和 this.setState`

#### 读取State
```
// class中
<p>You click {this.state.count} times</p>

// 函数组件中
<p>You clicked {count}</p>
```

#### 更新State
```
// 在class中
<button onClick={() => this.setState({ count: this.state.count + 1 })}>
    Click me
</button>

// 在函数组件中
<button onClick={() => setCount(count + 1)}>
    Click me
</button>
```

#### 为何使用方括号？
```
const [count, setCount] = useState(0)
```
这是一个数组结构的写法。意味着我们同时创建了count和setCount两个变量。
    - count的值是useState返回的第一个值
    - setCount的值是useState返回的第二个值
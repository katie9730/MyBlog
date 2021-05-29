## Context
Context提供了一个无需为每层组件手动添加显式props，就能在组件树间进行数据传递的方法。

#### 何时使用Context
Context设计目的是为了共享对于一个组件树而言是“全局”的数据。例如当前认证的用户、主题或首选语言。
```
const ThemeContext = React.createContext('light')
class App extends React.Component {
    render() {
        return (
            <ThemeContext.provider vlaue="dark">
                <Toolbar />
            </ThemeContext.provider>
        )
    }
}

function Toolbar() {
    return (
        <div>
            <ThemeButton />
        </div>
    )
}

class ThemeButton extends React.Component {
    static contextType = ThemeContext
    render() {
        return <Button theme={this.context} />
    }
}
```

## 未完待续 2021.5.17
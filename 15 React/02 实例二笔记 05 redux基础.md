### 介绍
Redux是一个数据状态管理插件，搭配React特别适合。类似于vue中的vuex。 

### 安装
`npm install redux react-redux --save`
```
// 第一步：定义计算规则，即reducer
function counter(state=0, action) {
    switch(action.type) {
        case 'INCREMENT':
            return state + 1
        case 'DECREMENT':
            return state - 1
        default:
            return state
    }
}

// 第二步：根据计算规则生成store
let store = createStore(counter)

// 第三步：定义数据(即state)变化之后的派发规则
store.subscribe(()=>{
    console.log('fn1 -> current state', store.getState())
})
store.subscribe(()=>{
    console.log('fn2 -> current state', store.getState())
})
 
// 第四步：触发数据变化
store.dispatch({type: 'INCREMENT'})
store.dispatch({type: 'INCREMENT'})
store.dispatch({type: 'DECREMENT'})
```
创建`store`用来管理数据，采用的是普通的发布和订阅的设计模式。
- 通过`dispatch`函数来触发数据的变化，触发的时候需要符合之前定制的规则，否则无效。
- 数据发生变化，即`subscribe`中定义的函数会执行。
- 通过`stroe.getState()`来获取当前的数据。

### Redux和React集成
- 第一步：创建store
```
const store = createStore(rootReducer, initialState,
    // 触发redux-devtools
    window.devToolsExtensin ? window.devToolsExtension() : undefined
)
// 第二个参数即初始化的数据，第三个参数可调起chrome扩展程序。
```
- 第二步：创建规则Reducer
`state`就是一个数据，可以进行`state+1`或`state-1`，数据结构较简单。若数据结构变复杂，必须分组管理。因此，可以用state.userinfo来表示用户数据，state.nav表四导航数据，state.ad表示广告数据...这就是用`combineReducers`分装各个reducer的作用。
- 第三步：创建action
- 第四步：结合到React
创建了`store`并传递给`<Provider>`组件，然后让`<Provider>`组件。
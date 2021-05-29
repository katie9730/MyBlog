#### 1.含义
为了减轻store对象过于臃肿。Vuex允许将store分割成模块。每个模块都拥有自己的state、mutation、action、getter。
```
const moduleA = {
    state:{},
    mutation:{},
    actions:{},
    getters:{}
    
}

const moduleB = {
    state:{},
    mutation:{},
    actions:{},
    getters:{}
}

const store = new Vuex.Store({
    modules:{
        a:moduleA,
        b:moduleB
    }
})

store.state.a // -> moduleA 的状态
store.state.b // -> moduleB 的状态
```

#### 2.模块的局部状态


## 未完待续 2019/9/12
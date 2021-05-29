#### 1.含义
Action类似于mutation，不同在于
+ Action提交的是mutation，而不是直接变更状态
+ Action可以包含任意异步操作
示例
```
const store = new Vuex.Store({
    state:{
        count:0
    },
    mutations:{
        increment(state){
            state.count++
        }
    },
    actions:{
        increment(context){
            context.commit('increment')
        }
    }
})
```

#### 2.分发Action
Action通过store.dispatch方法触发
`store.dispatch('increment')`
  
**action内部执行异步操作**
```
actions:{
    incrementAsync({commit}){
        setTimeout(()=>{
            commit('increment')
        },1000)
    }
}
```

**action以载荷形式分发**
```
store.dispatch('incrementAsync',{
    amount:10
})
```

**commit和dispatch的区别**
+ 在Mutation中使用commit且为同步操作`this.$store.commit('mutations方法名',值)`
+ 在Action中使用dispatch且为异步操作`this.$store.dispatch('mutations方法名',值)`


**action以对象形式分发**
```
store.dispatch({
    type:'incrementAsync',
    amount:10
})
```

**在组件中分发Action**    
你在组件中使用 this.$store.dispatch('xxx') 分发 action，或者使用 mapActions 辅助函数将组件的 methods 映射为 store.dispatch 调用（需要先在根节点注入 store）：

**组合Action**
```
// 假设 getData() 和 getOtherData() 返回的是 Promise

actions: {
  async actionA ({ commit }) {
    commit('gotData', await getData())
  },
  async actionB ({ dispatch, commit }) {
    await dispatch('actionA') // 等待 actionA 完成
    commit('gotOtherData', await getOtherData())
  }
}
```
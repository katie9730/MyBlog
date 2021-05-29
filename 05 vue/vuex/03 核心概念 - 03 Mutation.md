#### 1.含义
更改Vuex的store中的状态的唯一方法是提交mutation（类似事件）。    
mutation包含一个字符串的**事件类型（type）**和一个**回调函数（handler）**
```
const store = new Vuex.store({
    state:{
        count:1
    },
    mutations:{
        increment(state){
            //变更状态
            state.count++
        }
    }
})
```

#### 2.提交载荷（payload）
向store.commit传入额外的参数，称为mutation的载荷(payload)
```
mutations:{
    increment(state,n){
        state.count += n
    }
}

store.commit('increment',10)

```

#### 3.对象风格的提交方式
提交mutation的另一个方式是直接使用包含type属性的对象
```
store.commit({
    type:'increment',
    amount:10
})
```

#### 4.Mutation需遵守Vue的响应规则
Vuex的store状态是响应式的，当变更状态时，监视状态的Vue组件也会自动更新。
则需遵守的注意事项：
+ 提前在store中初始化好所需属性
+ 在对象上添加新属性时应使用Vue.set(obj,'newProp',123),或者以新对象替换老对象
```
state.obj = {...State.obj, newProp:123}
```

#### 5.使用常量替代Mutation事件类型    
使linter之类的工具发挥作用，同时把这些常量放在单独的文件中可以让你的代码合作者对整个app包含的mutation一目了然
```
// mutation-types.js
export const SOME_MUTATION = 'SOME_MUTATION'

// store.js
import Vuex from 'vuex'
import { SOME_MUTATION } from './mutation-types'

const store = new Vuex.Store({
  state: { ... },
  mutations: {
    // 我们可以使用 ES2015 风格的计算属性命名功能来使用一个常量作为函数名
    [SOME_MUTATION] (state) {
      // mutate state
    }
  }
})
```

#### 6.Mutation必须是同步函数
```
mutations:{
    someMutation(state){
        api.callAsyncMethod(()=>{
            state.count++
        })
    }
}
```

#### 7.在组件中提交Mutation    
在组件中使用this.$store.commit('xxx')提交mutation，
或者使用mapMutations辅助函数将组件中的methods映射为store.commit调用（需要在根节点注入store）。
```
impot { mapMutations } from 'vuex'
export default{
    methods：{
        ...mapMutations([
            'increment',  //将`this.increment()`映射为 `this.$store.commit('increment')`
            'incrementBy'  //将`this.incrementBy(amount)`映射为`this.$store.commit('incrementBy',amount)`
        ]),
        ...mapMutatins({
            add:'increment'  //将`this.add()`映射为`this.$store.commit('increment')`
        })
    }
}
```
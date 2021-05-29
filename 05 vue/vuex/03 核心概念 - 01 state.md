#### 1.单一状态树
Vuex使用单一状态数，用一个对象包含了全部的应用层级状态，且以一个“唯一数据源”而存在。可直接地定位特定的状态片段，在调试过程中轻易取得整个当前应用状态的快照。

#### 2.在Vue组件中获得Vuex状态
从store实例中读取状态最简单的方法就是计算属性中返回某个状态。
```
//创建一个Counter组件
const Counter = {
    template:`<div>{{ count }}</div>`,
    computed:{
        count(){
            return this.$store.state.count
        }
    }
}
//每当 store.state.count 变化的时候, 都会重新求取计算属性，并且触发更新相关联的 DOM。
```

**mapState 辅助函数**
当一个组件需要获取多个状态时，解决状态声明为计算属性产生的重复和冗余。
```
//单独构建的版本中辅助函数为Vuex.mapState
import {mapState} from 'vuex'

export default{
    computed:mapState({
        count:state => state.count,
        countAlias:'count',
        countPlusLocalState(state){
            return state.count + this.localCount
        }
    })
}

```

**对象展开运算符**
mapState函数返回的是一个对象。对象展开运算符，可以使用一个工具函数将多个对象合并为一个，使最终对象传给computed属性。
```
computed:{
    localComputed(){
        ...mapState({
            //...
        })
    }
}
```

**组件仍然保有局部状态**   
使用 Vuex 并不意味着你需要将所有的状态放入 Vuex。如果有些状态严格属于单个组件，最好还是作为组件的局部状态。

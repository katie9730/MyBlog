#### Getter   
getter类似计算属性，它的返回值会根据它的依赖被缓存起来，且只有当他的依赖值发生了改变才会被重新计算。  
Getter接受state作为其第一个参数
```
const store = new Vuex.Store({
    state:{
        todos:[
            {id:1,text:'...',done:true},
            {id:2,text:'...',done:false}
        ]
    },
    getters:{
        doneTodos:state =>{
            return state.todos.filter(todo => todo.done)
        }
    }
})
```
**通过属性访问**    
`store.getters.doneTodos // -> [{ id: 1, text: '...', done: true }]`

**通过方法访问**
```
getters:{
    getTodoById:(state) => (id) =>{
        return state.todos.find(todo => todo.id === id)
    }
}

store.getters.getTodoById(2)  //-> { id: 2, text: '...', done: false }

```  
注意：getter通过方法访问时，每次都会去进行调用，而不会缓存结果。

**mapGetters 辅助函数**   
将store中的getter映射到局部计算属性
```
import {mapGetters} from 'vuex'

export default {
    computed:{
        ...mapGetters([
            'doneTodosCount',
            'anotherGetter'
        ])
    }
}

//若想将getter属性另取一个名字，得使用对象形式    
mapGetters({
    //把this.doneCount映射为this.$store.getters.doneTodosCount
    doneCount:'doneTodosCount'
})

```

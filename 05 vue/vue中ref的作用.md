#### 1.基本用法，本页面获取dom元素
```
<template>
    <div id="app">
        <div ref="testDom">1111</div>
        <button @click="getTest">获取test节点</button>
    </div>
</template>
<script>
    export default{
        methods:{
            getTest(){
                console.log(this.$refs.testDom)
            }
        }
    }
</script>
```

#### 2.获取子组件中的data


#### 3.ref如果放在组件上，获取的是组件实例，而不是组件的dom元素
 #### 1.化繁为简的watch 
 watch是有字面量名称
 ```
 data(){
     return{
         value:null
     }
 }
 methods:{
     consoleDemo(){
         console.log('同学们好帅！')
     }
 }
 watch:{
     value:{
        // 表示创建组件的时候，立马执行一次。
         handler(newVal,oldVal){
             console.log(newVal);
             this.consoleDemo();
         },
         immediate:true
     }
 }
 ```
 
 #### 2.render函数的定义
 vue推荐在绝大多数情况下使用template来创建HTML。然而在一些场景中，我们需要JavaScript的完全编程能力，那就是render函数。render相比template更接近编译器。
 + 实质：render方法的实质就是生成template模板
 + 原理：通过调用一个方法，而这个方法是通过render方法的参数传递给他的。
 + 参数：这个方法有三个参数，分别提供标签名，标签相关属性，标签内部的html内容
 + 实现：通过这三个参数，可以生成一个完整的模板
 + 注意
    - 只限vue.js 2.x支持
    - render 方法可以使用JSX语法，但需要babel plugin插件
 ```
 [router.js]
 import Render from './views/render.vue'
 
 export default new Router({
     routes:[
        {
            path:'/render',
            name:'render',
            component:Render
        }
     ]
 })
 
 [render.vue]
 <template>
    <div class="hello">
        <h1>我是render组件</h1>
        <button :type="type" :text="text" @myEvent="parDemo"></button>
    </div> 
 </template>
 <script>
    import Button from './button.vue'
    export default{
        name:'HelloWorld',
        props:{
            msg:String
        },
        data(){
            return{
                value:2,
                type:'success',
                text:'绿色'
            }
        },
        components:{
          Button  
        },
        create(){
            
        },
        methods:{
            parDemo:function(){
                console.log('666');
            }
        }
    }
 </script>
 
 [button.vue]
 <srcipt>
 export default{
     props:{
         //按钮类型
         type:{
             type:String,
             default:'normal'
         }
         //文字
         text:{
             type:String,
             default:'demo'
         }
     },
     render(h){
         //创建元素
         return h('div',{
            //v-bind:class
             class:{
                 btn:true,
                 'btn-success':this.type === 'success',
                 'btn-success':this.type === 'danger',
                 'btn-success':this.type === 'warning',
             },
             //dom 属性
             domProps:{
                 innerText:this.text
             },
             on:{
                 click:this.demoClick
             }
         })
     },
     methods:{
         demoClick(){
             this.$emit('myEvent')
         }
     }
 }
 </script>
 ```
 
 #### 3.全局组件的引用
 ```
 [global.js]将所有需要全局注册的都放在这里
 import Vue from 'vue';
 function changeStr(str){
     return str.charAt(0).toUpperCase() + str.slice(1);
 }
 //
 const requireComponent = require.context('.',false,/\.vue$/);
 //keys 返回上下文模块可以处理的所有数组
 
 requireComponent.keys().forEach(fileName=>{
     const config = requireComponent(fileName);
     const componentName = changeStr(
        fileName.replace(/^\.\///,'').replace(/\.\w+$/,'')
     )
     Vue.component(componentName, config.default || config  )
 })
 
 [main.js]然后在main.js中引入Global
 import Global from './components/global.js'
 ```
 ```
 Vue.user(Router)
 //路由数组
 const routerList = [];
 function importAll(r){
     console.log(r.keys());
     r.keys().forEach(
        (key) => routerList.push(r(key).default)
     );
 }
 importAll(require.context('.',true,/\.routes\.js/));
 ```
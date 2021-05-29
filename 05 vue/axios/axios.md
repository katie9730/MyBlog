#### 1.使用
```
[main.js]
//引入
import Axios from 'axios';
//给Vue原型挂载一个属性，使所有的都对象都可以用这个
vue.prototype.$axios = Axios
```
```
[组件中]
export default {
    data(){
        return{
            data:[]
        }
    },
    created(){
        //get请求
        this.$axios.get('接口地址'),{
            params:{
                id:'123'
            }
        } 
        .then(res=>{
            this.data = res.data.message;
        })
        .catch(err=>{
            console.log(err);
        })
        
        //post请求
        this.$axios.post('接口地址'，{
            content:'霸气霸气'
        },{
            //设置
            headers:{
                'content-type':'application/x-www-form-urlencoded'
          }
        }
        )
        .then(res=>{
            this.data = res.data.message;
        })
    }
}


```
总结
+ post请求的时候，如果数据是字符串，默认头就是键值对，否则若是对象就是application/json
+ this.$axios.get(url,options)
+ this.$axios.post(url,data,options)
+ optins:{
    params:{  //查询字符串
        id:1
    },
    headers:{
        'content-type':'xxx'
    }
}
+ 全局默认设置： Axios.defaults.baseURL = 'xxx'

#### axios属性关系
    - options: headers、baseURL、params
    - 默认全局设置(大家都是这么用)
        + Axios.defaults-> options对象
    - 针对个别请求来附加options
    - axios.get(url,options)
    - axios.post(url,data,options)

#### 合并请求
+ axios.all([请求1，请求2])
+ 分发响应  axios.spread(fn)
+ fn:对应参数（res）和请求的顺序一致
+ 应用场景：
    - 必须保证两次请求都成功，比如分头获取省、市的数据
+ 执行特点：只要有一次失败就算失败，否则成功
```
function getMsg(res1,res2){
    console.log(res1);
    console.log(res2);
}

this.$axios.all([
    this.$axios.post('postcomment/300','content=123'),
    this.$axios.get('getcomments/300?pageindex=1')
])
//分发响应
.then(this.$axios.spread(getMsg))
.catch(err=>{
    console.log(err);
})

```


#### 拦截器
+ 过滤，在每一次请求与响应中，添油加醋
+ axios.interceptors.request.use(fn)   在请求之前
+ function(config){config.headers = {xxx}}   config相当于options对象
+ 默认设置 defaults 范围广、权利小
+ 单个请求的设置options get(url,options) 范围下、权利中
+ 拦截器 范围广 权利大

```
//默认设置
Axios.defaults.headers = {
    accept:'defaults'
}

//拦截器
Axios.interceptors.request.use(function(config){
    console.log(config);
    return config; //返回没有修改的设置，不return config就是一个拦截
    

    
    //个性化的修改
    //config.headers.accept = 'interceptors';
    config.headers = {
        accept:'interceptors'
    }
    
})
```

#### token（扩展）
+ 在cookie和session的机制，cookie自动带一个字符串
+ cookie只在浏览器
+ 移动端原生应用，也可以使用http协议，1：可以加自定义的头、原生应用没有cookie
+ 对于三端来讲，token可以作为类似cookie的使用，并且可以通用
+ 拦截器可以用在添加token上

```
//拦截器
Axios.interceptors.request.use(function(config){
    Mint.Indicator.open();
    //请求发起之前，显示loadding
    return config;
})

Axios.interceptors.response.use(function(data){
    Mint.Indicator.close();
    //在响应回来之后，隐藏loadding
    return data； 
})

```

#### 引入mint-ui
```
import Mint from 'mint-ui';  //export default 对应整个对象
import { Indicator } from 'mint-ui';  //export 对应整个对象.Indiactor
import 'mint-ui/lib/style.css';
//安装插件，注册一堆全局组件
Vue.use(Mint);
```

#### 解答
+ _this只是一个变量名，this代表父函数，如果在子函数还用this，this的指向就变成子函数了，_this就是用来存储指向的。
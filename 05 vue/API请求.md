#### 1.步骤+分析
第一步：确定api域名    
第二步：API地址 + 请求方式 + 返回的数据   
第三步：获取列表的分析
+ 1.由于已经导入了axios这个包，所以可以直接通过  this.$axios来发起数据请求
+ 2.根据接口API文档，知道获取列表的时候，应该发起一个get/post请求
+ 3.this.$axios.get('url').then(function(){}).catch(function(){})
+ 4.当通过then指定回调函数之后，在回调函数中，可以拿到数据服务器返回的result，通过.catch返回错误信息。(另外如果通过$http获取到的数据，都在**result.body**中放着)
+ 5.先判断result.status是否等于0(其中status根据API文档返回的参数而定)；如果等于0，就成功了，可以把result.message赋值给this.list；如果不等于0，可以弹框提醒，获取数据失败。
+ 6.当vm实例的data和methods初始化完毕后，vm实例会自动执行created这个生命周期函数。
```
created(){
    this.getAllList()
}
```

#### 2.实操
**1.添加功能**
```
[js中的methods]
   add(){
       this.$axios.get('47.98.148.203:7070/et-data/api/v1/dsl/exec/order_writeoff_list')
        .then(res=>{
            this.data = res.data.message;
        })
        .catch(err=>{
            console.log(err);
        })
   } 

        
```
**2.删除功能**
```
[html]
<a href="" @click.prevent='del(item.id)'>删除</a>
```
```
[js中的methods]
del(id){
    this.$axios.get('47.98.148.203:7070/et-data/api/v1/dsl/exec/order_writeoff_list' + id)
    .then(res=>{
        //删除成功
        this.getAllList();
    })
    .catch(err=>{
        alert('删除失败！')
    })
}

```
**3.全局配置数据接口的根域名**      
如果我们通过全局配置，请求数据接口根域名，则每次单独发起axios请求的时候，请求的url路径，应该以相对路径开头。
```
axios.defaults.baseURL = 'http://47.98.148.203:7070'  //配置默认根域名
axios.defaults.headers.common['Authorization'] = AUTH_TOKEN;  //headers添加对应的Token验证
axios.defaults.headers.post['Content-Type'] = 'application/x-www-form-urlencoded';  //配置表单默认的提交数据的格式
```

******
#### 3.数据交互
***JSON格式转化***    
JSON.stringify();

***fetch***
- fetch取代ajax
- 体验异步的终极解决方案ES7的Async/Await(学习这个的前提得学习es6与promise；在开发过程中,我们向服务端发送请求,一般会使用三种方式, XMLHttpRequest(XHR)，Fetch ，jQuery实现的AJAX。)

***Ajax***
- Ajax不是Javascript的规范，是一种用于创建快速动态网页的技术，XMLHttpRequest 是 AJAX 的基础。
   Ajax = 异步JavaScript 和 XML
- Web运作原理：一次HTTP请求对应一个页面
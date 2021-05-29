## promise
#### 作用
解决异步回调问题
#### 传统方式
大部分用回调函数，事件
```
ajax(url,{  // 获取token
    ajax(url,()=>{  // 获取用户信息
        ajax(url,()=>{ // 获取用户相关新闻
            …
        })
    })
})
```
#### promise语法
```
new Promise(function(resolve, reject{
    // resolve, 成功时调用
    // reject, 失败时调用
}))

promise.then(res=>{
    
},err=>{
    
})
```
#### 推荐用法
```
let p = new Promise().then(res=>{
    
}).catch(err=>{
    
})

Promise.resolve('aa')：将现有的东西，转成一个Promise对象，resolve状态，成功状态
等价于：
new Promise(resolve=>{
    resolve('aaa')
});

Promise.reject('aaa'):将现有的东西，转成一个promise对象，reject状态，失败状态
等价于：
new Promise((resolve, reject) =>{
    reject('aaa')
})

```
```
let p1 = Promise.resolve('aaa');
let p2 = Promise.resolve('bbb');
let p3 = Promise.resolve('ccc');

Promise.all([p1,p2,p3]).then(res=>{
    let [res1, res2, res3] = res;
    console.log(res1, res2, res3);
})

Promise.all([p1, p2, p3]):把promise打包，扔到一个数组里面，打包完还是一个promise对象，且必须确保，所有的promise对象,都是resolve状态，都是成功的状态 
```
Promise.rece([p1, p2, p3]):只要有一个成功了，就返回。

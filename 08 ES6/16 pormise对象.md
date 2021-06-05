# promise
## 1.含义
是异步编程的一种解决方案，比传统的的解决方案（回调函数和事件）更加合理和更强大。
简单说Promise就是一个容器，存放着某个未来才会结束的事件。
从语法上说，Promise是一个对象，用来获取异步操作的消息。
### Promise两个特点
- 对象的状态不收外界影响。只有异步操作的结果，能够决定状态，其他操作无法改变状态。
- 状态一旦改变，就无法再去改变，任何时候都是这个结果。状态改变的两种形式
    + pending -> fulfilled
    + pending -> rejected
### Promise缺点
- 一旦执行，立即执行，无法中途取消。
- 如果不设置回调函数，Promise内部抛出的错误，不会反映到外部。
- 处于pending状态，无法得知进展的如何了。

## 2.基本用法
ES6规定，Promise对象是一个构造函数，用来生成Promise实例。
```
const promise = new Promise(function(resolve, reject){
    if(/*异步操作成功*/){
        resolve(value)
    } else {
        reject(error)
    }
})

// 生成promise实例以后，可以使用then方法分别指定resolved或rejected的回调函数。
// then方法接受两个回调函数作为参数。
//    - 第一个回调函数是resolved时调用
//    - 第二个回调函数是rejected时调用
promise.then(function(){
    // success
}, function(){
    // failure
})

```
Promise构造函数接受一个函数作为参数，该函数的两个参数分别是resolve和reject。
- resolve: 将Promise对象的状态从“未完成”变成“成功”(pending -> resolved)
- reject: 将Promise对象的状态从“未完成”变成“失败”（pending ->rejected）

## 3.Promise.prototype.then()
then()方法是定义在原型对象Promise.prototype上的。它的作用是为Promise实例添加状态改变时的回调函数。
- 第一个参数：resolved状态回调
- 第二个参数：rejected状态的回调

## 4.Promise.prototype.catch()
用于指定发生错误时的回调函数。在then()方法指定的回调函数，若运行中抛出错误，就会被catch()方法捕获。
```
p.then((val)=>{
    console.log("fulfiled:", val)
}).catch((err)=>{
    console.log("rejected", err)
})
// 等同于
p.then((val)=> console.log('fulfilled:', val))
 .then(null, (err) => console.log('rejected', err))
```
- 建议使用catch()方法捕获错误，而不使用then()方法的第二个参数。
- Promise内部的错误不会影响到Promise外部代码，通俗的说法是“Promise会吃到错误”

## 5.Promise.prototype.finally()
finally()方法用于指定不管Promise对象最后状态如何，都会执行操作。该方法是ES2018引入的标准。
filally()方法的回调函数不接受任何参数。这表明，finally方法里面的操作，应该是状态无关的，不依赖Promise的执行结果。
```
promise
.then(result => {...})
.catch(error => {...})
.finally(() => {...})
```

## 6.Promise.all()
Promise.all()方法用于将多个Promise实例，包装成一个新的Promise实例。
```
const p = new Promise.all([p1, p2, p3])
// Promise.all()方法接受一个数组作为参数，p1、p2、p3都是Promise实例。如果不是，则先调用Promise.resolve方法，将参数转为Promise实例，再进一步处理。
// Promise.all()方法的参数可以不是数组，但必须具有Iterator接口，且返回的每个成员都是Promise实例。

// p的状态有p1、p2、p3决定,分为2种情况
- p1、p2、p3的状态都变成fulfilled,p的状态才会变成fulfilled,此时p1、p2、p3的返回值组成一个数组，传递给p的回调函数。
- 只要p1、p2、p3有个rejeced，p的状态就是变成rejected，此时第一个被reject的实例的返回值，会传递给p的回调函数。

// 假如p1有自己的catch方法，那么就会调用自己的catch()方法，不然就会调用Promise.all()中的catch方法。
```

## 7.Promise.race()
Promise.race()方法同样是将多个Promise实例，包装成一个新的Promise实例。
```
const p = Promise.race([p1, p2, p3])
// p1、p2、p3之中有一个实例率先改变状态，p的状态就发生改变。率先改变的Promise实例的返回值，就是传递给p的回调函数。
```

## Promise.allSettled()
Promise.allSettled()方法接受一组Promise实例作为参数，包装成一个新的Promise实例。只要等到所有这些参数实例返回结果，不管是fulfilled还是rejeced，包装实例才会结束。——引入自ES2020
```
const promise = [
    fetch('/api-1'),
    fetch('/api-2'),
    fetch('/api-3')
]
await Promise.allSettled(promises)
removeLoadingIndicator()
```
该方法返回的新的Promise实例，一旦结束，状态就是fulfilled，不会变成rejected。状态变成fulfilled后，Promise的监听函数接收到的参数是一个数组，每个成员对应一个传入Promise.allSettled()的Promise实例。

## Promise.any（）



******
## 传统方式
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
## promise语法
```
new Promise(function(resolve, reject{
    // resolve, 成功时调用
    // reject, 失败时调用
}))

promise.then(res=>{
    
},err=>{
    
})
```
## 推荐用法
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

#### 1.概述
promise对象是JavaScript的异步操作解决方案，为异步操作提供统一接口。它起到代理作用(proxy)，充当异步操作与回调函数之间的中介，使得异步操作具备同步操作的接口。promise可以让异步操作写起来，就像在写同步操作的流程，而不必一层层的嵌套回调函数。
```
//首先，Promise是一个对象，也是一个构造函数。
function f1(resolve,reject){
    //异步代码
}

var p1 = new Promise(f1);
//promise构造函数接受一个回调函数f1作为参数，f1里面是异步操作的代码。然后返回的p1是一个Promise实例。
```
**设计思想**   
所有异步任务都返回一个promise实例，Promise实例有一个then方法，用来指定下一步的回调函数
```
var p1 = new Promise(f1);
p1.then(f2);
//先执行f1的异步操作，再执行f2。
```
传统的写法需要把f2作为回调函数传入f1，比如携程f1(f2),异步操作完成后，在f1内部调用f2。Promise使得f1和f2变成链式写法。改善了连续性，对于多层嵌套的回调函数尤其方便。
```
//传统写法
step1((value1)=>{
    step2((value2)=>{
        step3((value3)=>{
            //...
        })
    })
})
//promise写法
(new Promise(step1))
    .then(step2)
    .then(step3)
    .then(step4);
```  
目前JavaScript原生支持Promise对象。


#### 2.Promise对象的状态   
promoise对象通过自身的状态，来控制异步操作。Promise实例具有三种状态。且状态变化只能发生一次。
+ 异步操作未完成（pending）
+ 异步操作成功（fulfilled）
+ 异步操作失败（rejected）   
其中fulfilled和rejected合在一起称为resolved（已定型）。
   
变化途径（两种）
+ 从“未完成”到“成功”
+ 从“未完成”到“失败”   

最终结果（两种）
+ 异步操作成功，Promise实例传回一个值（value），状态变为fulfilled。
+ 异步操作失败，Promise实例抛出一个错误（error），状态变成rejected。

#### 3.Promise 构造函数   
JavaScript提供原生的Promise构造函数，用来生成Promise实例。
```
var Promise = new Promise((resolve,reject)=>{
    //...
    
    if(/*异步操作成功*/){
        resolve(value);
    }else{
        reject(new Error());
    }
})

//Promise构造函数接受函数作为参数（resolve和reject），这两个函数，由JavaScript引擎提供，不用自己实现。
```

#### 4.Promise.prototype.then()   
Promise实例的then方法，用来添加回调函数。then方法接受两个回调函数，成功时调用fulfilled状态的回调函数；失败时调用rejected状态的回调函数。   
then方法可以链式使用。
```
p1
    .then(step1)
    .then(step2)
    .then(step3)
    .then(
        console.log,
        console.error
    )
//上面代码中，p1后面有四个then，意味依次有四个回调函数。只要前一步的状态变为fulfilled，就会依次执行紧跟在后面的回调函数。

//最后一个then方法，回调函数是console.log和console.error，用法上有一点重要的区别。console.log只显示step3的返回值，而console.error可以显示p1、step1、step2、step3之中任意一个发生的错误。举例来说，如果step1的状态变为rejected，那么step2和step3都不会执行了（因为它们是resolved的回调函数）。Promise 开始寻找，接下来第一个为rejected的回调函数，在上面代码中是console.error。这就是说，Promise 对象的报错具有传递性。
```

#### 5.then用法解析
+ 写法一：f3回调函数的参数，是f2函数的运行结果。
```
f1().then(function () {
  return f2();
}).then(f3);
```
+ 写法二：f3回调函数的参数是undefined。
```
f1().then(function () {
  f2();
  return;
}).then(f3);
```
+ 写法三：f3回调函数的参数，是f2函数返回的函数的运行结果。
```
f1().then(f2())
  .then(f3);
```
+ 写法四：写法四与写法一只有一个差别，那就是f2会接收到f1()返回的结果。
```
f1().then(f2)
  .then(f3);
```
#### 6.实例：图片加载       
iamge是图片对象的实例。他有两个事件监听属性，onload属性在图片加载成功后调用，onerror属性在加载失败调用。
```
var preloadImage = function(path){
    return new Promise(function(resolve,reject){
        var image = new Image();
        image.onload = resolve;
        image.onerror = reject;
        image.src = path;
    })
}
```
   
preloadImage()函数用法如下
```
preloadImage('https://example.com/my.jpg')
  .then(function (e) { document.body.append(e.target) })
  .then(function () { console.log('加载成功') })
```

#### 7.小结
**Promise优点**    
+ 让函数变成链条写法，流程清晰
+ 可实现许多强大的功能。比如，执行多个异步操作，等状态改变后，再执行回调函数；再比如多个回调函数抛出错误，可以统一指定处理方法。
+ 状态一旦改变，无论何时查询，都能得到这个状态。

**Promise缺点**
+ 编写难度高
+ 阅读代码也不是一眼就能看懂，需要理清逻辑

#### 8.微任务    
Promise的回调函数属于异步任务，在同步任务之后执行。但Promise不是正常的异步任务，而是微任务。区别在于，正常的任务追加到下一轮事件循环，微任务追加到本轮事件循环。意味着，微任务的执行时间早于正常任务。
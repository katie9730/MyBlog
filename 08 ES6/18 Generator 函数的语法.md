## generator函数
他是一个生成器，用来解决异步，深度嵌套的问题，async

#### 语法
```
function * show(){
    
}

// 定义：
function * gen(){
    yield 'welcome';
    yield 'to';
    return '牧马人';
}
// 调用,这类手动调用，略麻烦些
let g1 = gen();
g1.next(); // {value:'welcome', done:false}
g1.next(); // {value:'to', done:false}
g1.next(); // {value:'牧马人', done:true}
```
for...of可以自动遍历generator;return的东西，它就不会遍历
+ generator可以配合for...of
+ 解构赋值扩展：let [a,...b] = gen();
+ 扩展运算符：`...`
+ Arrar.from()：eg`console.log(Array.from(gen()))`;
+ generator结合axios数据请求
*** 
异步：不连续，上一个操作没有执行完，下一个操作照样开始
同步：连续执行，上一个操作没有执行完，下一个没法开始

关于异步，解决方案
+ 回调函数
+ 事件监听
+ 发布/订阅
+ Promise对象
    


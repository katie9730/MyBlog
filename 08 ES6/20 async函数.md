***
#### ES2017规定了async
nodejs的fs.readFile用来读取文件
1. promise
2. generator
3. async

```
async function fn(){  // 表示异步，这个函数里面有异步任务
    let result = await xxx // 表示后面结果需要等待
    
}
```
#### async特点
1. await只能放到async函数中
2. 相比geneator语义化更强
3. wait后面可以是promise对象，也可以是数字、字符串、布尔值
4. async函数返回的是一个promise对象
5. 只要await语句后面的promise状态变成reject，那么整个async函数会中断执行。

#### 解决async函数中抛出错误，影响后续代码
```
// 方式一（建议使用这个）
    try{
        
    }catch(e){
        
    }
    
    // 例如
    try{
        let f1 = await readFile('data/a.txt')
        let f2 = await readFile('data/b.txt')
        let f3 = await readFile('data/c.txt')
    }catch(e){
        
    }
    
// 方式二
    promise本身有catch
```
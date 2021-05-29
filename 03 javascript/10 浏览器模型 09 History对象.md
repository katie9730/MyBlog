#### 1.概述   
指向History对象，它表示当前窗口的浏览历史。History对象保存了当前窗口访问过的所有页面网址。由于安全原因，浏览器不允许脚本读取地址，但是允许地址之间导航。
```
window.history.length 

//后退到前一个网址
history.back()
//等同于
history.go(-1)
```
#### 2.属性
+ History.length：当前窗口访问过的网址数量
+ History.state：History堆栈最上层的状态值

#### 3.方法
**3.1 History.back()、History.forward()、History.go()**
+ History.back()：移动到上一个网址
+ History.forward()：移动到下一个网址
+ History.go()：接受一个整数作为参数，以当前网址为基准，移动到参数指定的网址

**3.2 History.pushState()**    
用于历史中添加一条记录
```
window.history.pushState(state, title, url)
// state:一个与添加的记录相关联的状态对象。
// title：新页面的标题
// url：新的网址
```

**3.3 History.replaceState()**
用来修改History对象的当前记录，其他和History.pushState()方法一模一样

#### 4.popstate事件    
每当同一个文档的浏览历史（即history对象）出现变化时，就会触发popstate事件。注意，仅仅调用pushState()方法或replaceState()方法 ，并不会触发该事件。

## EventTarget接口     
事件的本质是程序各个组成部分之间的一种通信方式，也是异步编程的一种实现。

#### 1.概述
DOM的事件操作（监听和触发）都定义在EventTarget接口。所有节点对象都部署在这个接口，其他一些需要事件通信的浏览器内置对象（XMLHttpRequest、AudioNode、AudioContext）也都部署在这个接口。    
这个接口主要提供了三个实例方法
+ addEventListener:绑定事件的监听函数
+ removeEventListener:移除事件的监听函数。
+ dispatchEvent：触发事件

#### 2.EventTarget.addEventListener()
```
target.addEventListener(type,listener[,useCapture]);
```
该方法接受三个参数
+ type：事件名称，大小写敏感。
+ listener：监听函数。事件发生时，会调用该监听函数。
+ useCapture：布尔值。表示监听函数是否在捕获阶段触发，默认为false。除了布尔值，还可以是一个属性配置对象。该对象有以下属性。
    - capture：布尔值，表示该事件是否在`捕获阶段`触发监听函数。
    - once：布尔值，表示监听函数是否只触发一次，然后就自动移除。
    - passive：布尔值，表示监听函数不会调用事件的preventDefault方法。

#### 3.EventTarget.removeEventListener()   
用来移除addEventListener方法添加的事件监听函数。该函数没有返回值。其他与addEventListener()参数一致。

#### 4.EventTarget.dispatchEvent()   
此方法在当前节点上触发指定事件，从而触发监听函数的执行。该方法返回一个布尔值，只要有一个监听函数调用了Event.preventDefault(),则返回false，否则返回true。    
dispatchEvent方法的参数是一个Event对象的实例。
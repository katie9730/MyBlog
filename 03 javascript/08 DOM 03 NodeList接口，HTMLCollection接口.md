### NodeList接口，HTMLCollection接口   
节点都是单个对象，有时候需要一种数据结构，容纳多个节点。
Dom提供两种节点集合，用于容纳多个节点：NodeList和HTMLCollection，它们的区别在于
+ NodeList:可以包含各种类型的节点
+ HTMLCollection：只能包含HTML元素的节点。

#### 1.NodeList接口
**1.1 概述**   
类似数组的对象，但又不是数组，可以使用length属性和forEach方法，但是不能使用pop或者push这种，数组特有的方法。成员是节点对象。通过以下方法可以得到NodeList实例。
+ Node.childNodes
+ document.querySelectorAll()   
如果NodeList实例要使用方法，可以将其转为真正的数组。
```
var children = document.body.childNodes;
var nodeArr = Array.prototype.slice.call(children);
```

**1.2 NodeList.prototype.length**   
返回NodeList实例包含的节点数量。
```
document.querySelectorAll('xxx').length
```
**1.3 NodeList.prototype.forEach()**   
用于遍历NodeList的所有成员。接受一个回调函数作为参数。
```
var children = document.body.childNodes;
children.forEach(function f(item,i,list){
    //...
},this);
```
**1.4 NodeList.prototype.item()**   
接受一个整数值作为参数，表示成员的位置，返回该位置上的成员。
```
document.body.childNodes.item(0)
```

**1.5 NodeList.prototype.keys(),NodeList.prototype.values(),NOdeList.prototype.entries()**    
这三个方法都返回一个ES6的遍历对象，通过for...of循环遍历获取每一个成员信息。区别在于
+ keys():返回键名的遍历器
+ values():返回键值得遍历器
+ entries():同时返回键名和键值信息。


#### 2.HTMLCollection接口
**2.1 概述**  
+ 是一个节点对象的集合，只能包含元素节点，不能包含其他类型的节点。
+ 类似数组的对象，不过它没有forEach方法，只能使用for循环遍历。

**2.2 HTMLCollection.prototype.length**   
返回HTMLCollection实例包含的成员数量。
```
document.links.length // 18
```
**2.3 HTMLCollection.prototype.item()**   
接受整数值作为参数，表示成员的位置，返回该位置上的成员
```
var c = document.images;
var img0 = c.item(0);
```

**2.4 HTMLCollection.prototype.namedItem()**
参数是一个字符串，表示id属性或者name属性的值，返回对应的元素节点。若没有，返回null。

## 完结 2019/6/20
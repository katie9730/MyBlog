## 1.Set
#### 基本用法
Set是ES6提供的新的数据结构。类似数组。
+ 特点一：每个成员的值都是唯一的，没有重复。  
+ 特点二：Set本身是一个构造函数，用来生成Set数据结构。
```
const s = new Set();
[2,3,5,4,5,2,2].forEach(x => s.add(x));

for (let i of s){
    console.log(i);
}
// 2 3 5 4
```
+ 特点三：Set函数可以接受一个数组作为参数，用来初始化
```
const set = new Set([1, 2, 3, 4, 4])
[...set]
// [1, 2, 3, 4]
```
+ 特点四：向Set加入值时，是不会发生类型转换的，所以`5`和`'5'`是不同的值，类似于精确相等运算符（===）。主要的区别是向 Set 加入值时认为NaN等于自身，而精确相等运算符认为NaN不等于自身。

#### Set实例的属性和方法
##### 属性  
+ Set.prototype.constructor:构造函数，默认就是Set函数
+ Set.prototype.size：返回Set实例的成员总数
##### 方法（两类）
- 操作方法（用于操作数据）
    + Set.prototype.add(value):添加某个值，返回Set结构本身
    + Set.prototype.delete(value):删除某个值，返回一个布尔值，表示删除是否成功
    + Set.prototype.has(value):返回一个布尔值，表示该值是否为Set成员
    + Set.prototype.clear():清除所有成员，没有返回值
- 遍历方法（用于遍历成员）
    + Set.prototype.keys():返回键名的遍历器
    + Set.prototype.values():返回键值的遍历器
    + Set.prototype.entries():返回键值对的遍历器
    + Set.prototype.forEach():返回回调函数遍历每个成员

## 2.WeakSet()
#### 含义
与Set类似。不过与Set也有区别。
+ 区别一：WeakSet的成员只能是对象，不能使其他类型的值。
+ 区别二：WeakSet对象是弱引用，即垃圾回收机制不考虑WeakSet对该对象的引用。可以用来保存DOM节点，不容易造成内存泄漏
+ 区别三：WeakSet适合临时存放一组对象且ES6规定WeakSet不可遍历，是因为成员可能随时都会消失，遍历机制无法保证成员的存在。

#### 语法
WeakSet是一个构造函数，可以使用new命令，创建WeakSet数据结构。
```
const ws = new WeakSet();
```
**方法**
+ WeakSet.prototype.add(value):向WeakSet实例添加一个新成员。
+ WeakSet.prototype.delete(value):清除WeakSet实例的指定成员。
+ WeakSet.prototype.has(value):返回一个布尔值，表示某个值是否在WeakSet实例之中。

## Map
#### 含义和基本用法
JavaScript的对象，本质上是键值对的集合（Hash结构），但在传统上只能用字符串当作键。
+ 本质上是键值对的集合，类似集合
+ 可以遍历，方法多，可以跟各种数据格式转换

## WeakMap
+ 只接受对象作为键名（null除外），不接受其他类型作为键名
+ 键名所指向的对象，不计入垃圾回收机制
+ 不能遍历，方法同get、set、has、delete
## 未完待续 2019/10/29


***
#### set用法
```
// 定义
let setArr = new Set(['a','b'])

// 方法
setArr.add('a'); 往setArr里面添加一项
setArr.delete('b'); 删除一项
setArr.has('a'); 判断setArr里面有没有此值
setArr.size; 个数
setArr.clear();清空
```
#### for...of
+ for(let item of setArr){console.log(item)}   // 默认是values
+ for(let item of setArr.keys()){...}
+ for(let item of setArr.values()){...}
+ for(let [k,v] of setArr.entries()){}

#### 数组去重
```
let arr = [1,2,3,5,6,4,3,4,3,3,2,1]
let newArr = [...new Set(arr)];
console.log(newArr);
```
#### set数据结构变成数组
[...set]

#### set()与weakSet()的区别
+ new Set([]);  存储数组，这种写法对
+ new WeakSet({}); 存储json，这种写法不太靠谱
    - WeakSet有add(),has(),delete();没有size，clear()
    - 初始化时往里面添加东西是不行的，最好使用add方法添加

***
#### map
类似json，但是json的键（key）只能是字符串
map的key可以是任意类型

#### map的使用
```
let map = new Map();
map.set(key.value);  // 设置一个值
map.get(key) // 获取一个值
map.delete(key) // 删除一项
map.has(key) // 判断有没有
map.clear() // 清空
```
#### map的循环
```
for(let [key,value] of map){}
for(let key of map.keys()){}
for(let value of map.values()){}
for(let [k,v]) of map.entries(){}
```

#### WeakMap()
key只能是对象

#### 总结
+ Set里面是数组，不重复，没有key,没有get方法
+ Map对json功能增强，key可以是任意类型的值
#### 1.let命令
***基本用法***   
let命令用来声明变量，类似var，不过let命令只会在所在代码块内有效。
```
{
  let a = 10;
  var b = 1;
}

a // ReferenceError: a is not defined.
b // 1
```

***不存在变量提升***    
var命令会发生‘变量提升’现象，如果变量在声明之前使用，值是undefined。
然后let纠正了这种现象，let规定，声明变量一定要在声明后使用的，否则会报错。
```
// var 的情况
console.log(foo); // 输出undefined
var foo = 2;

// let 的情况
console.log(bar); // 报错ReferenceError
let bar = 2;
```

***暂时性死区***   
若块级作用域内存在let命令，它声明的变量就会‘绑定’这个区域，不再受外部的影响。所有就算外部全局定义了块级作用域内的变量，是失效的。
```
var tmp = 123;

if (true) {
  tmp = 'abc'; // ReferenceError
  let tmp;
}
```   
注意：'暂时性死区'意味着typeof不再是一个百分之百安全的操作。
```
typeof x; // ReferenceError
let x;
//上面代码中，变量x使用let命令声明，所以在声明之前，都属于x的“死区”，只要用到该变量就会报错。因此，typeof运行时就会抛出一个ReferenceError。若这个变量根本没有被声明，使用typeof反而不会报错。
```
总结： 
ES6 规定暂时性死区和let、const语句不出现变量提升，主要是为了减少运行时错误，防止在变量声明前就使用这个变量，从而导致意料之外的行为。

***不允许重复声明***    
let不允许在相同作用域内，重复声明同一个变量，因此不能再函数内部重新声明参数。

***关于let、var*** 
+ let、var都为声明变量。let声明的变量只在let命令所在的代码块内有效及私有作用域。var声明变量是全局有效。
+ let变量一定要在声明后使用。
+ 不管函数还是let定义的变量都不可以重复定义
+ 虽然不进行预解释，但是代码执行前上来也是先将定义的变量提前过滤一遍，一旦发现不合法的直接报错，代码也不会执行了。
+ 注意eval将字符串转为对象的时候，一定要加一个()
```
//使用var时，显示undefined,表示只声明未定义
console.log(a);
var a=1;

//使用let时，显示not defind，表示没有提前声明（没有预解释）
console.log(a);
let a=1;
```

#### 2.块级作用域    
##### 为什么需要块级作用域  
ES5有全局作用域和函数作用域，没有块级作用域。

##### ES6的块级作用域
let为JavaScript新增了块级作用域，且允许作用域任意嵌套，每层作用域互不影响。

##### 块级作用域与函数声明
+ ES5规定，函数只能在顶层作用域和函数作用域之中声明，不能在块级作用域声明。
+ ES6引入了块级作用域，允许块级作用域之中声明函数。且块级作用域必须有大括号`{}`是一个私有作用域
```
function fn(){
    let a=0;
    console.log(a);
}

if(){};
for(){};
```

#### 3.const
***基本用法***
+ 只读常量，一旦声明，常量的值不可改变。
+ 一旦声明，必须赋值，否则报错`Missing initializer in const declaration`
+ 只对声明所在的块级作用域内有效
+ 常量不提升，存在暂时性死去
+ 不可以重复声明的（不管是动态变量还是静态变量都是不可以重复定义） 
+ Object.freeze方法可以将对象冻结。

***ES6声明变量的六种方法***
+ ES5只有两种声明变量的方法：var命令和function命令
+ ES6除了添加let和const命令，另外还有import命令和class命令。

#### 4.顶层对象的属性
+ 在浏览器中指的是window对象
+ 在Node中指的是global对象
+ ES5中，顶层对象属性等价于全局变量（顶层对象的属性与全局变量挂钩，被认为是 JavaScript 语言最大的设计败笔之一）。ES6为了改进这点，且保持兼容性，var命令和function命令声明的全局变量，依旧是顶层对象的属性；let命令、const命令、class命令声明的全局变量，不属于顶层对象的属性。也就是说，ES6开始，全局变量逐步与顶层对象属性脱钩。


#### 5.globalThis对象
JavaScript语言存在一个顶层对象，用来提供全局环境，所以代码都在这个环境 中运行。但是，顶层对象在各种实现里面是不统一的。
+ 浏览器中，顶层对象是window，但Node和Web Worker没有window。
+ 浏览器和Web Worker中，self也指向顶层对象，但Node没有self。
+ Node里面，顶层对象是global，但其他环境不支持。
为了在各种环境中，都能取到顶层对象，一般是使用this变量，但是它是很局限性的。所以有一个提案，建议引入`globalThis`作为顶层对象。

******
完结 2019/9/10








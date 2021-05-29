#### 1.概述
+ 由于ES5的对象属性名都是字符串，就会造成属性名额冲突。所以ES6引入Symbol的原因，表示独一无二的值。    
+ JavaScript语言的第七种数据类型，前六种是:undefined、null、布尔值、字符串、数值、对象。   
+ Symbol值通过symbol函数生成。那么对象的属性名就可以有两种类型，一种是字符串，一种是新增的Symbol类型。凡是属性名属于Symbol类型的，都是独一无二的。
+ Symbol值不能与其他类型的值进行运算，可以转为字符串、布尔值，但不能转为数值。
+ symbol不是构造函数，所以不能使用new命令。
+ 当symbol的参数为一个对象时，它就会自动调用该对象的toString方法，将其转为字符串，在生成Symbol值。
+ symbol值不能与其他类型的值进行运算，会报错。

#### 2. Symbol.prototype.description
```
// 创建Symbol可以为他添加一个描述,下面sym的描述就是字符串foo
const sym = Symbol('foo');

// 通过实例属性description，直接返回Symbol描述
const sym = Symbol('foo');
sym.description //'foo'
```

#### 3.作为属性名的Symbol

## 未完待续 2019/11/11
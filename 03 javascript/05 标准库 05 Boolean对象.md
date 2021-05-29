#### 1. 概述
Boolean对象是JavaScript的三个包装对象之一。作为构造函数，它主要用于生成布尔值的包装对象实例。
```
var b = new Boolean(true)

typeof b // 'object'
b.vlaueOf() // true
// b是一个Boolean对象的实例，它的类型是对象，值为布尔值true。
```

#### 2.Boolean函数的类型转换作用
Boolean对象除了可以作为构造函数，还可以单独使用，将任意值转为布尔值。另外双重的否运算符`(!)`也可以将任意值转为对应的布尔值。
```
Boolean(1) // true
!!1 // true

// 以下是特殊情况
if (Boolean(false)) {
  console.log('true');
} // 无输出

if (new Boolean(false)) {
  console.log('true');
} // true

if (Boolean(null)) {
  console.log('true');
} // 无输出

if (new Boolean(null)) {
  console.log('true');
} // true
```
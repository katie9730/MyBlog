## 1.简介
#### 类的由来
```
// 传统方法通过构造函数生成实例对象
function Point(x,y){
    this.x = x;
    this.y = y;
}

Point.prototype.toString = function(){
    return '(' + this.x + ',' + this.y + ')';
};

var p = new Point(1,2);

// ES6引入class（类）这个概念，作为对象的模板，生成实例对象。
// es6的类可以看作是构造函数的另一种写法
class Point{
    constructor(x, y){
        this.x = x;
        this.y = y;
    }
    toString(){
        return '(' + this.x + ',' + this.y + ')';
    }
}

// 类的数据类型是函数，类本身就指向构造函数
typeof Point // 'function'
Point === Point.prototype.constructor // true

// ES6的“类”保留了构造函数的prototype属性。且类的所有方法都定义在类的prototype属性上面。所以在类的实例上面调用方法，其实就是调用原型上的方法。
class Point{
    construcotr(){}
    toString(){}
    toValue(){}
}
等同于
Point.prototype = {
    constructor(){},
    toString(){},
    toValue(){},
}

// 唯一与ES5行为不一致的是类的内部所有定义的方法都是不可枚举的。
```
#### constructor方法
constructor方法是类的默认方法，通过new命令生成对象实例是，自动调用该方法。一个类必须有constructor方法，计算没有，也会被默认添加上去。
```
类必须使用new调用，否则会报错，这也是他跟普通构造函数的一个主要区别，后者不用new也可以执行。
class Foo{
    constructor(){
        return Object.create(null);
    }
}

Foo() // TypeError: Class constructor Foo cannot be invoked without 'new '
```
#### 类的实例
与ES5一样，实例的属性除非显式定义在其本身（即定义在this对象上），否则就都定义在原型上（即定义在class上）。
```
//定义类
class Point {

  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  toString() {
    return '(' + this.x + ', ' + this.y + ')';
  }

}

var point = new Point(2, 3);

point.toString() // (2, 3)

point.hasOwnProperty('x') // true
point.hasOwnProperty('y') // true
point.hasOwnProperty('toString') // false
point.__proto__.hasOwnProperty('toString') // true
```
与ES5一样，类的所有实例共享一个原型对象
```
var p1 = new Point(2,3);
var p2 = new Point(3,2);
p1._proto_ === p2._proto_  // true
// p1和p2都是Point实例，所以他们的原型都是Point.prototype，所以_proto_属性都是相等的。注意，因为`_proto_`是会改写原型，影响到所有实例，所以并不太推荐使用这个。
```
#### 取值函数（getter）和存值函数（setter）
getter和setter是设置在属性的Descriptor对象上的。与ES5一样，在“类”的内部可以使用get和set关键字，对某个属性设置存值函数和取值函数，拦截该属性的存取行为。
```
class Person{
    constructor(){
        
    }
    get aaa(){
        return `aaa的属性`;
    }
    set aaa(val){
        console.log(`设置aaa属性，值为：${val}`);
    }
}
let p1 = new Person();
p1.aaa = '123';
console.log(p1.aaa);
```

#### 属性表达式
类的属性名，可以采用表达式
```
let methodName = 'getArea'
class Square {
    constructor(length){
        
    }
    [methodName](){
        
    }
}
```
#### class 表达式
与函数一样，类也可以使用表达式的形式定义
```
const MyClass = class Me{
    getClassName(){
        return Me.name;
    }
}
// 上面代码使用表达式定义了一个类，这个类的名字是Me
// Me只在Class的内部可用，指代当前类
// 在Class外部，这个类智能用MyClass引用

let inst = new MyClass();
inst.getClassName() // Me
Me.name // ReferenceError: Me is not defined
```

#### 注意点
+ 严格模式：在类和模块的内部，默认使用严格模式，所有不需要使用`use strict`指定运行模式
+ ES6中的class不存在提升；ES5中，用函数模拟可以提升的，因为函数默认有提升效果
+ name属性：本质上ES6的类只是ES5的构造函数的一层包装，所以函数的许多特性都被Class继承，包括name属性
```
class Point {}
Point.name  // 'Point'
```
+ Generator方法：如果某个方法前加上型号（`*`），就表示该方法是一个Generator函数
```
class Foo {
    constructor(...args){
        this.args = args;
    }
    *[Symbol.iterator](){
        for(let arg of this.args){
            yield arg;
        }
    }
}
```
+ this的指向：类的方法内部如果含有this，则默认指向类的实例，不过单独使用该方法，可能会报错。解决方法是在构造方法中绑定this。
    - 矫正this的三种方式：fn.call(), fn.apply(), fn.bind()
    - 1.fn.call(this指向谁，args1, args2…)
    - 2.fn.apply(this指向谁，[args1, args2…])
    - 3.fn.bind()

## 2.静态方法
静态方法就是类身上的方法，类相当于实例的原型，所有在类中定义的方法，都会被实例继承。如果在一个方法前，加上`static`关键字，就表示该方法不会被实例继承，而是直接通过类来调用的，这就称为“静态方法”。
```
class Foo {
    static classMethod(){
        return 'hello';
    }
}
Foo.classMethod() // 'hello'；静态方法只能被类调用，不能被实例调用
var foo = new Foo();
foo.classMethod() // TypeError:foo.classMethod is not function

```
+ 注意1：如果静态方法包含this关键字，这个this指的是类，而不是实例。
+ 注意2：且静态方法可以和非静态方法重名。
+ 注意3：父类的静态方法，可以被子类继承。

## 3.实例属性的新写法
实例属性除了定义在constructor()方法里面的this上面，还可以定义在类的最顶层。它的好处，看上去一目了然，一眼就能看出那些是实例属性。
```
class IncreasingCounter{
    constructor(){
        this._count = 0;
    }
    get value(){
        console.log('Getting the current value!');
        return this._count;
    }
    increment(){
        this._count++;
    }
}
// 新写法
class IncreasingCounter{
    _count = 0;
    get value(){
        console.log('Getting the current value!');
        return this._count;
    }
    increment(){
        this._count++;
    }
}

```
## 4.静态属性
静态属性指的是Class本身的属性，即Class.propName，而不是定在实例对象（this）上的属性。
```
// 老写法
class Foo{
    
} 
Foo.prop = 1;
Foo.prop // 1

// 新写法
class MyClass {
    static prop = 42;
}
```

## 5.私有方法和私有属性
#### 现有的解决方案
私有方法和私有属性是只能在类的内部访问的方法和属性，外部不能访问。有利于代码的封装，但ES6不提供，只能通过变通方法模拟实现。
```
// 做法一：在命名上加以区分
class Widget{
    // 公有方法
    foo(baz){
        this._bar(baz);
    }
    
    // 私有方法:`_baz`方法前面的下划线，表示这是一个只限于内部使用的私有方法。但这种命名并不保险，在类的外部，还是可以调用到这个方法。
    _baz(baz){
        return this.snaf = baz;
    }
}

// 做法二：索性将私有方法移除模块
class Widget{
    foo(baz){
        bar.call(this, baz);
    }
}

function bar(baz){
    return this.snaf = baz;
}

// 做法三：利用Symbol值得唯一性，将私有方法的名字命名为Symbol值
const bar = Symbol('bar');
const snaf = Symbol('snaf');

export default class myClass{
    // 公有方法
    foo(baz){
        this[bar](baz);
    }
    
    // 私有方法
    [bar](baz){
        return this[snaf] = baz;
    }
}
```

#### 私有属性的提案
目前有个提案，为class加私有属性。方法是在属性名之前，使用#表示。
```
// 只可在内部访问，外部访问会报错
class IncreasingCounter {
    #count = 0;
    get value(){
        console.log('Getting the current value!');
        return this.#count;
    }
    increment(){
        this.#count++
    }
}
```

## new.target属性
new是一个构造函数生成实例对象的命令。ES6为new命令引入了一个new.target属性，该属性一般用在构造函数之中，返回new命令作用于那个构造函数。这个属性可以用来确定构造函数是怎么调用的。当子类继承父类时，new.target则会返回子类。
```
class Shape {
  constructor() {
    if (new.target === Shape) {
      throw new Error('本类不能实例化');
    }
  }
}

class Rectangle extends Shape {
  constructor(length, width) {
    super();
    // ...
  }
}

var x = new Shape();  // 报错
var y = new Rectangle(3, 4);  // 正确
```
## 完结 2019/10/31

#### 以下是来自网易云视频的概念补充
es5写法
```
function Person(name, age){
    this.name = name;
    this.age = age;
}
// Object.assign方法用于对象的合并，将源对象（source）所有可枚举属性，复制到目标对象（target）
// 语法：Object.assign(target, source1, source2);
Object.assign(Person.prototype,{
    showName(){
        return `名字为:${this.name}`;
    },
    showAge(){
        return `年龄为：${this.age}`;
    }
})
let p1 = new Person('Strive', 18);
console.log(p1.showName());
console.log(p1.showAge());
```
es6写法
```
let a = strive

class Person{
    constructor(){ // 构造方法(函数),调用new的时候自动执行
        
    }
    [a](){ // 表示是这个函数的一个变量
        return `中括号是定义变量的意思`
    }
}
let p1 = new Person('strive', 18)
console.log(p[a]) //与console.log(p.strive)相等
```
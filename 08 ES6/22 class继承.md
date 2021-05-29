## 1.简介
Class通过extends关键字实现继承，这比ES5通过修改原型链实现继承，要清晰和方便的多。
```
class Point{
}

class ColorPoint extends Point {
}

// ColorPoint类通过extends关键字，继承了Point类所有的属性和方法。
```
ES5的继承，实质是先创造子类的实例对象this，然后将父类的方法添加到this上面（parent.apply(this)）。    
ES6的继承机制完全不同，实质是将父类实例对象的属性和方法加到this上面，然后再用子类的构造函数修改this。

+ 注意点一：子类的构造函数，必须调用super之后，才能使用this关键字，否则就会报错。
+ 注意点二: 父类的静态方法，也会被子类继承。

## 2.Object.getPrototypeOf()
该方法用于从子类上获取父类，因此可以使用这个方法来判断，一个类是否继承了另一个类。
```
Object.getPrototypeOf(ColorPoint) === Point
```
## 3.super关键字
既可以当作函数使用，也可以当作对象使用。
+ 作为函数调用，代表父类的构造函数。ES6规定，子类构造函数必须执行一次super函数。否则就会报错。
```
class A{}
class B extends A {
    constructor(){
        super();
    }
}
```
+ 作为对象时，在普通方法中，指向父类的原型对象；在静态方法中，指向父类。

## 未完待续 2019/10/31

#### 以下是来自网易云视频的概念补充
ES5继承的写法
```
// 父类
function Person(name){
    this.name = name;
}
Person.prototype.showName = function(){
    return `名字是：${this.name}`
}

// 子类
function Student(name, skill){
    Person.call(this, name); // 继承属性
    this.skill = skill;
}
Student.prototype = new Person(); // 继承方法

// 调用
let stu1 = new Student('strive','逃学')
console.log(stu1.name)
```
ES6继承的写法
```
// 父类
class Person{
    constructor(name){
        this.name = name;
    }
    showName(){
        return `名字为：${this.name}`
    }
}

// 子类
class student extends Person{
    constructor(name, skill){
        super(name); // super指向了父级的构造函数，将父级的属性都继承过来
        this.skill = skill;
    }
    showName(){
        super.showName(); // super指向了父级的构造函数，调用父级的方法
        console.log('子类里的showName') // TODO自己的事情
    }
    showSkill(){
        return `哥们儿的技能为：${this.skill}`;
    }
}

// 调用
let stu1 = new Student('strive','逃学')
console.log(stu1.showSkill());

```
```
1.安装：npm install -g typescript
2.编译：tsc helloworld.ts
3.Typescript开发工具 VScode自动编译.ts文件：
第一步： tsc --init 生成tsconfig.json 改 “outDir” ：“./js”
第二步： 任务 --运行任务  点击  tsc:监视-tsconfig.json  然后就可以自动生成代码
4.任意类型 any
5.void类型:表示没有类型
function run():void{
console.log('run');
}
run();
6.never类型：其他类型，（包括null和undefined）的子类型，代表从不会出现的值。这意味着声明never的变量只能被never类型所赋值。

二：函数定义(函数名定义法)
1.//函数声明
function run(){
return 'run';
}
//匿名函数
var run2 = function(){
return 'run2';
}
2.方法可选参数
//es5里面方法的实参和形参可以不一样，但是ts中必须一样，如果不一样就需要配置可选参数。



//三点运算符   接受新参传过来的值（剩余参数）

3.ts函数的重载
//java中方法的重载：重载指的是两个或者两个以上同名函数，但它们的参数不一样，这时会出现函数重载的情况
//typescript中的重载，通过为同一个函数提供多个函数类型定义来试下多种功能的目的。
//ts为了兼容es5 以及es6重载的写法和java中有区别




4.箭头函数（this指向问题   箭头函数里面的this指向上下文）


三.es5中的类

*实例方法一定要new一下才能被调用。静态方法不用new就可以调用。

*原型链实现继承
原型链实现继承：可以继承构造函数里面的属性和方法，也可以继承原型链上面的属性和方法

*原型链+构造函数的组合继承模式

```
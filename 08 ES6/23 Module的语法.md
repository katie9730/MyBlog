#### 1.概述    
在历史上，JavaScript没有模块体系。在ES6之前，制定模块加载方案，主要是基于CommonJS（用于服务器）和AMD（用于浏览器）。ES6中实现了模块功能，完全取代了CommonJS和AMD规范，称为浏览器和服务器通用的模块解决方案。

ES6模块的设计思想是尽量的静态化，使编译时就能确定依赖关系，及输入输出变量。CommonJS和AMD模块则是在运行时确定这些东西。ES6的编译时加载，可以拓宽JavaScript语法，比如引入宏（Macro）和类型检验（type system）这些只能靠静态分析实现的功能。
```
//CommonJS模块
let { stat, exists, readFile } = require('fs')
//整体加载fs模块（即加载fs的所有方法），生成一个对象（_fs）,然后在着这个对象上读取3个方法。这种加载称为“运行时加载”，即在运行时才能得到这个对象，无法在编译时做到“静态优化”。

//ES6模块(ES6模块不是对象，通过export命令显式输入，通过import命令输入)
import {stat, exists, readFile} from 'fs';
//从fs模块加载3个方法，其他不加载。这种加载称为“编译时加载”或“静态加载”，即ES6在编译时完成模块加载，效率高于CommonJS。
//弊端：无法引用ES6模块本身，因为它不是对象。
```
除了静态加载带来各种好处，ES6模块还有以下好处：
+ 不再需要UMD模块格式了，将来服务器和浏览器都会支持ES6模块格式。目前，通过各种工具库，其实已经做到了这一点。
+ 将来浏览器的新 API就能用模块格式提供，不再必须做成全局变量或者navigator对象的属性。
+ 不再需要对象作为命名空间（比如Math对象），未来这些功能可以通过模块提供。

#### 2.严格模式（严格模式是ES5引入的，详情见ES5文档）
ES6**自动采用严格模式**。不管头部是否加上'use strict'。   
严格模式主要有以下限制：
+ 变量必须声明后再使用
+ 函数的参数不能有同名属性，否则报错
+ 不能使用with语句
+ 不能对只读属性赋值，否则报错
+ 不能使用前缀 0 表示八进制数，否则报错
+ 不能删除不可删除的属性，否则报错
+ 不能删除变量delete prop，会报错，只能删除属性delete global[prop]
+ eval不会在它的外层作用域引入变量
+ eval和arguments不能被重新赋值
+ arguments不会自动反映函数参数的变化
+ 不能使用arguments.callee
+ 不能使用arguments.caller
+ 禁止this指向全局对象
+ 不能使用fn.caller和fn.arguments获取函数调用的堆栈
+ 增加了保留字（比如protected、static和interface）

注意：this的限制。ES6模块中，顶层的this指向undefined，即不应该在顶层代码使用this。

#### 3.export命令
模块功能主要由两个命令构成：export和import。
+ export：用于规定模块的对外接口
+ import：用于输入其他模块提供的功能。   

import和export命令会被JavaScript引擎静态分析，会先于模块内的其他模块执行，所以只能在模块的顶层，不能再代码之中。
  
一个模块是一个独立的文件。外部无法获取内部所有变量。不过你可以通过export输出该变量。例如：
```
//profile.js
export var firstName = 'michael';
export var lastName = 'Jackson';
export var year = 1958;
//ES6将profile.js视为一个模块，用export命令对外部输出三个变量。

//另一种写法(推荐)
var firstName = 'Michael';
var lastName = 'Jackson';
var year = 1958;
export {firstName, lastName, year}
```
export除了输出变量，还可以输出函数或类
```
export function multiply(x,y){
    return x*y;
}
//输出一个函数 multiply
```
通常情况下，export输出的变量是本来的名字，不过也可以使用as关键字重命名
```
function v1(){...}
function v2(){...}

export{
    v1 as streamV1,
    v2 as streamV2,
    v2 as streamLatestVersion
}
//使用as关键字，重命名了函数v1和v2的对外接口。重命名后，v2可以用不同的名字输出两次。
```
注意：export命令规定的是对外接口，必须与模块内部的变量建立一对一对应关系。export的三种写法(function和class也必须遵守)：
```
//写法一
export var m = 1;

//写法二
var m = 1;
export {m};

//写法三
var n = 1;
export {n as m};
```
export语句输出的接口，与值是动态绑定的。即通过该接口，可以取到模块内部实时的值。与CommonJS规范完全不同。CommonJS模块输出的值得缓存，不存在动态更新。
```
export var foo = 'bar';
setTimeout(() => foo = 'baz' ,500);
```
最后，export命令可以出现在模块的任何位置，只要处于模块顶层就可以。如果处于块级作用域内，就会报错，下一节的import命令也是如此。这是因为处于条件代码块之中，就没法做静态优化了，违背了 ES6 模块的设计初衷。
```
function foo() {
  export default 'bar' // SyntaxError
}
foo()
//export语句放在函数之中，结果报错。
```

#### 4.import命令
使用export命令定义了模块的对外接口后，就可以通过import命令加载这个模块了。
```
//main.js
import { firstName, lastName, year } from './profile.js';

function setName(element){
    element.textContent = firstName + '' + lastName；
}
//用import命令，加载profile.js文件，并从中输入变量。大括号内的变量名，必须与被导入模块（profile.js）对外接口的名称相同。
```
import命令要使用as关键字，将输入的变量重命名。
```
import { lastName as surname } from './profile.js';
```

import命令输入的变量是只读的，不允许在加载模块的脚本里面，改写接口。
```
import {a} from './xxx.js'
a = {}; //Syntax Error : 'a' is read-only;
a.foo = 'hello'; //合法操作
//a的属性可以成功改写，且其他模块可以读到改写后的值。不过不便查错，所以不建议这样操作。
```

import后面的from是用来指定模块文件的位置（相对路径，绝对路径都可），.js后缀可省略。若是模块名，只需有配置文件，且不需要带路径地址即可。例如
```
import {myMethod} from 'util';
```
注意
+ 1.import命令具有提升效果。
+ 2.由于import是静态执行，那么它不能使用表达式和变量（只能在运行时才能有这样的语法结构）。
+ 3.CommonJS模块的require命令和ES6模块的import，不建议写在同一模块中。
+ 4.import可以是相对路径，也可以是绝对路径。
+ 5.import模块只会导入一次，无论你引入多少次。

#### 5.模块的整体加载
```
// circle.js

export function area(radius) {
  return Math.PI * radius * radius;
}

export function circumference(radius) {
  return 2 * Math.PI * radius;
}
```
```
//指定加载
import { area, circumference } from './circle';

//整体加载
import * as circle from './circle'
```

#### 6.export default命令   
模块文件`export-default.js`默认输出为一个函数。当其他模块加载该模块时，import命令可以为该匿名函数指定任意名字。
```
// export-default.js
export default function(){
    console.log('foo');
}

import customName from './export-default';
customName();
```
默认输出与正常输出的比较
```
//默认输出(不需要使用大括号，因为一个模块显然只有一个默认输出，所以也不能跟变量声明语句)
export default function crc32(){};
import crc32 from 'crc32';

//正常输出(需要使用大括号，可以使用声明语句)
export function crc32(){}

import {crc32} from 'crc32'
```
export default也可以用来输出类
```
// MyClass.js
export default class {...}

//main.js
import MyClass from 'MyClass';
let o = new MyClass();
```
#### 7.export与import的复合写法
如果在一个模块之中，先输入后输出同一个模块，import语句可以与export语句写在一起。    
注意：写成一行以后，foo和bar实际上并没有被导入当前模块，只是相当于对外转发了这两个接口，导致当前模块不能直接使用foo和bar。
```
export { foo, bar } from 'my_module';

// 可以简单理解为
import { foo, bar } from 'my_module';
export { foo, bar }
```
模块接口改名和整体输出
```
// 接口改名
export { foo as myFoo } from 'my_module';
// 整体输出
export * 'my_module';
```
默认接口的写法如下
```
// 默认接口的写法如下。
export { default } from 'foo'

// 具名接口改为默认接口的写法如下。
export { es6 as default } from './someModule';

import { es6 } from './someModule';
export default es6;
```

#### 8.模块的继承
假设circleplus模块继承circle模块。
```
[circleplus.js]
export * from 'circle';
export var e = 2.71828182846
export default function(x){
    return Math.exp(x);
}

// export *表示输出circle模块的所有属性和方法。但是export * 命令会忽略circle模块的default方法。

```


## 未完待续 2019/9/19







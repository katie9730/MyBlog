***js与node***

1. js返回的是浏览器配置，node返回的是系统的配置
    - 在ECMAScript部分node和js其实是一样的。比如数据类型的定义，语法结构，内置对象
    - 在js中顶层对象：window；在node中的顶层对象：global，注意：在node中也没有什么window。
2. 在node.js中有一个规定，一个文件就是一个模块，每个模块都有自己的作用域。我们使用var来申明的一个变量，他并不是全局的，而是属于当前模块下的。
```
eg1:var a=100;
    console.log(a);  // a=100; 这个属于模块中变量

eg2:global.a=200;
    console.log(global.a);   //a=200;   这个属于全局中定义的变量

eg3:console.log(__filename)：当前文件被解析过后的绝对路径。且属于当前模块下的。
```
3. 模块加载机制 使用require('模块')
```
eg1：require(’./2.js‘);   //此为相对路径
     require('b:/录制视频/NodeJS/课件/module/2.js');   //此为绝对路径
     require(’2.js‘)   //若不写点号啥的，他就会加载node中的核心模块，或者是node_modules文件夹内

eg2：require('./2')
    1.首先按照加载的模块的文件名称进行查找。
    2.如果没有找到，则会在模块文件名称后加上.js的后缀，进行查找。
    3.如果还没有找到，则会在文件名称后加上.json的后缀，进行查找。
    4.如果还没有找到，则会在文件名称后加上.node的后缀，进行查找。
    文件名称->.js->.json->.node->报错
```
4. 在一个模块中通过var定义的变量，其作用域范围是是当前模块，外部不能够直接的访问，如果我们想一个模块能够访问另外一个模块定义的变量，可以：
    1. 把变量作为global对象的一个属性，但是这样的做法不推荐
    2. 使用模块对象 module  ,他是用来保存提供 各当前 模块有关的一些信息.在这个 module对象中,有现代战争子对象:exports对象,我们通过这个 对象把一个模块中的局部变量对象进行提供访问.
    ```
    //eg1
    var a=100;
    module.exports.a = a;
    //eg2
    var m5 = require('./5');
    console.log(m5);
    
    ```
    3. 在模块作用域,还有一个内置的模块对象,exports,他其实就是module.exports
    ```
    var a=100;
    exports.a = a;
    //:exports和module.exports的指向关系已经断开了,宁可添加关系也不要这样去指向关系，如下
    module.exports = [1,2,3];
    exports.a = 200;
    ```
    
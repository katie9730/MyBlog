### 1.构造函数
Array是JavaScript的原生对象，且是构造函数，可以生成新的数组。但是Array作为构造函数，行为很不一致。不建议生成新的数组，直接使用数组字面量是更好的做法
```
//生成新的数组，不推荐
var arr = new Array(2)

//直接使用数组字面量，推荐
//等号左边为变量名，等号右边为字面量
var arr = [1,2]
```
**字面量**   
概念：固定值的量，字面是什么含义就是什么量。     
分类：数字字面量，字符串字面量，undefined(未定义的量)，布尔值字面量（true,false）

### 2.静态方法
Array.isArray():返回布尔值，表示参数是否为数组
```
//Array.isArray()弥补typeof运算符不足
//typeof只能识别它是一个对象
//Array.isArray()可以识别出它是数组
var arr = [1,2,3];
typeof arr // "object"
Array.isArray(arr)
```
### 3.实例方法
**3.1 valueOf(),toString() --> 都是对象的通用方法**
+ valueOf():返回数组本身。
```
var arr = [1,2,3];
arr.valueOf() //[1,2,3]
```
+ toString()：返回数组的字符串形式
```
var arr = [1,2,3];
arr.toString() //'1,2,3'
```

**3.2 push(),pop() -->都会改变原数组**
+ push():用于在数组的末端添加元素，并返回新数组的长度。
+ pop():用于删除数组的最后一个元素，并返回该元素。该方法会改变原数组。
```
//push()与pop()结合使用，构成‘后进先出’的栈结构
//push()与shift()结合使用，构成‘先进先出’的队列结构
var arr = [];
arr.push(1, 2);
arr.push(3);
arr.pop();
arr // [1, 2]
//注意：[].pop() 返回的是undefined

```

**3.3 shift(),unshift()**
+ shift():删除数组第一个元素，并返回该元素
+ unshift():在数组的第一个位置添加元素，并返回数组长度。可添加多个参数。

**3.4 join()**   
用于指定参数为分隔符，且以字符串返回。若无参数，默认以逗号分隔。
```
var a = [1,2,3,4];
a.join('') //'1 2 3 4'
a.join('|') //'1|2|3|4'
a.join() //'1,2,3,4'
```
**3.5 concat()**    
用于多个数组的合并，从原数组的后部添加。返回新数组。
```
['hello'].concat(['world']) //['hello','world']
```
**3.6 reverse()**   
用于颠倒排列数组的元素
```
var a = ['a','b','c']
a.reverse() // ['c','b','a']
a //['c','b','a']
```
**3.7 slice()**   
用于提取目标数组一部分，返回新数组
`arr.slice(start,end)`
```
var a = ['a','b','c']
a.slice(0,1) //['a']
//注意1：若参数为负数，则表示倒数计算位置
//注意2：如果第一个参数大于等于数组长度，或者第二个参数小于第一个参数，则返回空数组。

```

**3.8 splice()**   
用于删除原数组的一部分成员，且在删除的位置添加新的数组成员，且返回被删除的元素。
`arr.splice(start,count,addElement1,addElement2,...)`
```
var a = ['a','b','c','d','e','f']
a.splice(4,2) //['e','f']
a // ['a','b','c','d']
```

**3.9 sort()**
对数组成员，默认按照字典顺序排序
```
['d', 'c', 'b', 'a'].sort()
// ['a', 'b', 'c', 'd']
```

**3.10 map()**
将数组的所有成员历遍，执行语句，并返回新的数组
```
var numbers = [1,2,3];
numbers.map((n)=>{
    return n+1;
}) //[2,3,4]


[1, 2, 3].map(function(elem, index, arr) {
  return elem * index;
});
// [0, 2, 6]
//map方法的回调函数有三个参数，elem为当前成员的值，index为当前成员的位置，arr为原数组（[1, 2, 3]）

```
**3.11 循环总结**
> 循环结构的执行步骤
1.声明循环变量
2.判断循环条件
3.执行循环体操作
4.更新循环变量
5.然后循环执行2-4，直到条件不成立，跳出循环

**3.11.1 while循环，do-while循环**
1. while循环
> 特点：先判断再执行
```
var num = 1;   //1.声明循环变量
while (num <= 10){  //2.判断循环条件
    document.write(num + '<br />');  //3.执行循环体操作
    num++; //4.更新循环变量
}
```
2. do-while循环
> 特点：先执行再判断，即使条件不成立，do-while至少执行一次
```
var num = 10;
do{
    document.write(num + '<br />')  //10 9 8 7 6 5 4 3 2 1 0
    num--；
}while(num>=0);
document.write(num);  //-1   
```

**3.11.2 for(), for-in(), forEach(), for-of()**
1. for()   
特点：先判断后执行，与while相同
```
for (var num =1; num<=10; num++) {
    document.write(num+" <br />"); //1 2 3 4 5 6 7 8 9 10 
}

```
2. for-in()---(效率低)    
特点：主要用于历遍对象。效率极低，为其他循环的1/7。不仅遍历数组中的元素，还会遍历自定义的属性，甚至原型链上的属性都被访问到。且遍历数组元素的顺序可能是随机的。   
格式: `for(keys in zhangsan){}`   
keys表示obj对象的每个键值对的键。
obj[keys]表示obj对象的每个键值对的值。
for-in循环，可以读取对象自身上的成员属性。也可以遍历是否是对象的原型属性。使用hasOwnProperty可以判断出属性是不是对象自身上的属性。
eg：obj.hasOwnProperty(keys)==true。表示是对象的成员属性，而不是原先属性。
```
//声明一个Peson类
function Person(){
    this.name = "张三";
    this.age = 14;
    this.func1 = function(){
        
    }
}
//实例化这个类
var zhangsan = new Person();
//使用for-in遍历这个对象
for(keys in zhangsan){
    console.log(zhangsan[keys])
}
```
3. forEach()---(不能break、continue和return)   
特点：不能break、continue和return，不会跳过undefined和null，但会跳过空位。用法基本与map()相同，唯一不同的是，它不返回值，只是用来操作数据。    
```
function log(element,index,array){
    console.log('[' + index + '] = ' + element);
}

[2,5,9].forEach(log);
//[0] = 2
//[1] = 5
//[2] = 9
```
4. for-of()---(ES6新增方法)    
特点：作为遍历所有数据结构的统一方法。for...of循环内部调用的是数据结构的Sysbol.iterator方法。
+ 【数组】
for...in循环可直接获得对象的键名，不能直接获取键值。
ES6 提供for...of循环，允许遍历获得键值。
```
var arr = ['a','b','c','d'];
for (let a in arr){
    console.log(a); //0 1 2 3
}

for (let a of arr){
    console.log(a); //a b c d
}

```
+ 【Set和Map结构】   
set结构遍历时，返回的是一个值。map结构遍历时，返回的是一个数组，该数组的两个成员分别是当前Map成员的键名和键值。
```
var engines = new Set(['Gecko','Trident','Webkit','Webkit']);
for (var e of engines){
    console.log(e);
}
//Gecko Trident Webkit

var es6 = new Map();
es6.set('edition',6);
es6.set('committee','ECMA-262');
es6.set('standard','ECMA-262');
for(var [name,value] of es6){
    console.log(name + ':' + value);
}
// edition: 6
// committee: TC39
// standard: ECMA-262

```

+ 【类似数组的对象】   
下面是for...of循环用于字符串、DOM NodeList对象、arguments对象的例子。
```
// 字符串
        var str = "hello";
        
        for (let s of str) {
          console.log(s); // h e l l o
        }
        
        // DOM NodeList对象
        let paras = document.querySelectorAll("p");
        
        for (let p of paras) {
          p.classList.add("test");
        }
        
        // arguments对象
        function printArgs() {
          for (let x of arguments) {
            console.log(x);
          }
        }
        printArgs('a', 'b');// 'a' 'b'
```

5. 历遍语法的比较    
> for...in循环有几个缺点    
　　①数组的键名是数字，但是for...in循环是以字符串作为键名“0”、“1”、“2”等等。    
　　②for...in循环不仅遍历数字键名，还会遍历手动添加的其他键，甚至包括原型链上的键。    
　　③某些情况下，for...in循环会以任意顺序遍历键名。    
　　for...in循环主要是为遍历对象而设计的，不适用于遍历数组。    
> for...of循环       
　　有着同for...in一样的简洁语法，但是没有for...in那些缺点。    
　　不同于forEach方法，它可以与break、continue和return配合使用。    
　　提供了遍历所有数据结构的统一操作接口。    

6. 循环控制语句  
>  1、break：跳出本层循环，继续执行循环后面的语句。
　 如果循环有多层，则break只能跳出一层。 

> 2、continue：跳过本次循环剩余的代码，继续执行下一次循环。    
　①对与for循环，continue之后执行的语句，是循环变量更新语句i++；     
　②对于while、do-while循环，continue之后执行的语句，是循环条件判断；     
　因此，使用这两个循环时，必须将continue放到i++之后使用，否则，continue  将跳过i++进入死循环。  
　
```
for(var i = 1; i < 10; i++){
    if(i == 4){
        continue;
    }
    console.log(n);//1 2 3 5 6 7 8 9
}

for(var i = 1; i < 10; i++){
    if(i == 4){
        break;
    }
     console.log(i);//1 2 3
}
```

**3.12 filter()**
+ 用于过滤数组成员，满足条件者返回新数组。
+ filter()方法可以接受三个参数：当前成员(elem)，当前位置(index)和整个数组(arr)
```
[1,2,3,4,5].filter(function(elem){
    return (elem > 3);
})
//[4,5]

[1,2,3,4,5].filter((elem,index,arr)=>{
    return index % 2 ===0;
})
//[1,3,5]
```

**3.13 some(),every()**
+ some():只要一个成员返回值是true，则整个some方法返回值就是true。
+ every():所有成员返回值是true，结果才返回true，否则为false。
+ 注意：对于空数组，some方法返回fasle，every方法返回true，回调函数都不会执行。
```
var arr = [1,2,3,4,5];
arr.some((elem,index,arr)=>{
    return elem >=3;
})
//true


var arr = [1,2,3,4,5];
arr.erver((elem,index,arr)=>{
    return elem >=3;
})
//false
```

**3.14 reduce(),reduceRight()**
+ 依次处理数组的每个成员，最终累计为一个值。ruduce()是从左往右，ruduceRight是从右往左。（可用这个方法找出字符长度最长的数组成员）
+ 这两个方法，第一个参数都是函数，且该函数接受4个参数。
    - 累积变量（必填）：默认为数组的第一个成员
    - 当前变量（必填）：默认为数组的第二个成员
    - 当前位置（从0开始，选填）
    - 原数组（选填）
+ 第二个参数可对累积变量指定初值。由于空数组取不到初始值，reduce方法就会报错。加上第二个参数，就能保证它总是会返回一个值。
```
[1,2,3,4,5].reduce((a,b)=>{
    return a+b;
},10);
//25
//10是累积变量的初值，所以数组从10开始累加，最终结果为25
//注意，这是b是从数组的第一个成员开始遍历的。
```

**3.15 indexOf(),lastIndexOf()**
+ indexOf():返回数组中第一次出现的位置，没有则返回-1。第二个参数，表示搜索的开始位置
```
var a = ['a','b','c'];
a.indexOf('b') //1
a.indexOf('y') //-1
a.indexOf('a',1) //-1
```
+ lastIndexOf():返回数组中最后一次出现的位置，没有则返回-1。
```
var a = [2,5,9,2];
a.lastIndexOf(2) //3
a.lastIndexOf(7) //-1
```
+ 这两个方法不能用来搜索NAN的位置。因为这两个方法内部使用了严格相等运算符（===），而NAN是唯一一个不等于自身的值。

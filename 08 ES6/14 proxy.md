## 1.概述
proxy指的是代理（又称代理器），用于外界对某个对象架设一层“拦截”，在访问时进行过滤和改写。
```
var obj = new Proxy({},{
    get: function (target, key, receiver) {
        console.log(`getting ${key}!`);
        return Reflect.get(target, key, receiver);
    },
    set: function (target, key, value, receiver) {
        console.log(`setting ${key}!`);
        return Reflect.set(target, key, value, receiver);
    }
})
```
Proxy实例也可以作为其他对象的原型对象
```
var proxy = new Proxy({},{
    get:function(target, property){
        return 35;
    }
})

let obj = Object.create(proxy);
obj.time //35
```

## 2.Proxy实例的方法
#### 2.1 get(目标对象,属性名,proxy实例本身)
用于拦截某个属性的读写操作

## 未完待续 2019/10/23


***
+ proxy(代理)：扩展增强对象的一些功能
+ proxy作用：比如vue中的拦截、预警、上报、扩展功能、统计、增强对象等
+ proxy是设计模式的一种，即代理模式。
```
let obj = {
    name:'Strive'
};
// 您访问了name
obj.name // Strive
```
+ proxy的语法
```
new Proxy(target, handler);

let obj = new Proxy(被代理的对象，对代理的对象做什么操作)

handler:{
    set(){}, // 设置的时候干的事情
    get(){}, // 获取干的事情
    deleteProperty(){}, // 删除
    has(){} // 问你有没有这个东西 'xxx' in obj
    apply() // 拦截方法
    ...
}
```
```
// 实现一个，访问一个对象身上属性，默认不存在的时候给undefined，希望如果不存在错误（警告）信息。
let obj = {
    name:'Strive'
}

let newObj = new Proxy(obj,{
    get(target, property){
        if(property in target){
            return target[property];
        }else{
            console.warn(`${property}属性不在对象上`);
        }
    }
})
```
+ Reflect.apply(调用的函数，this指向，参数数组)
    - fn.call()
    - fn.apply() 类似
    - Reflect：反射
```
Reflect：反射
    Object.xxx语言内部方法。例如Object.defineProperty
    放到Reflect对象身上
    通过Reflect对象身上直接拿到语言内部东西
    `assign` in Object -> Reflect.has(Object,'assign');
    delete json.a -> Reflect.deleteProperty(json,'a');
```
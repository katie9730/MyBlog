#### 1.概述  
Storage接口用于脚本在浏览器保存数据。window.sessinStorage和window.localStorage。
+ sessionStorage：保存的数据用于浏览器的一次会话，当会话结束，数据就被清空。
+ localStorage:保存的数据长期存在，下一次访问的时候也还在。    
 
注意：这两者除了保存期限不同，其他方面都一样。localStorage类似Cookie的强化版。

#### 2.属性和方法
**2.1属性**    
+ Storage.length：返回保存的数据项个数。
```
window.localstorage.setItem('foo','a');
window.localstorage.setItem('foo','a');
window.localstorage.setItem('foo','a');
window.localstorage.length   //3
```
**2.2方法**
+ Storage.setItem():用于存入数据。接受两个参数，第一个是键名，第二个是保存的数据。且都是字符串。
```
window.localStorage.foo = '123';
window.localStorage['foo'] = '123';
window.localStorage.setItem('foo', '123');
```
+ Storage.getItem():用于读取数据。只有键名一个参数。若键名不存在，则返回null。
+ Storage.removeItem():用于清除某个键名对应的键值。若键名为空，则没有任何操作。
+ Storage.clear():用于清除所有保存的数据，返回值是undefined。
```
window.sessionStorage.clear()
```
+ Storage.key()：接受一个整数作为参数,返回该位置对应的键值。
```
window.sessionStorage.setItem('key','value')
```
#### 3.storage事件
Storage接口储存的数据发生变化时，会触发storage事件，可以指定这个事件的监听函数。
```
window.addEventListener('storage',onStorageChange);
```    
监听函数接受一个event实例对象作为参数。这个实例对象继承了 StorageEvent 接口，有几个特有的属性，都是只读属性。

+ StorageEvent.key：字符串，表示发生变动的键名。如果 storage 事件是由clear()方法引起，该属性返回null。
+ StorageEvent.newValue：字符串，表示新的键值。如果 storage 事件是由clear()方法或删除该键值对引发的，该属性返回null。
+ StorageEvent.oldValue：字符串，表示旧的键值。如果该键值对是新增的，该属性返回null。
+ StorageEvent.storageArea：对象，返回键值对所在的整个对象。也说是说，可以从这个属性上面拿到当前域名储存的所有键值对。
+ StorageEvent.url：字符串，表示原始触发 storage 事件的那个网页的网址。
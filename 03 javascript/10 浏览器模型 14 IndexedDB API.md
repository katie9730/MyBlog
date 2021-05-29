#### 1.概述
将大量数据储存在客户端，减少从服务器获取数据，直接从本地获取数据。由于Cookie和localStorage都不适合储存大量数据，且不提供搜索功能，所以IndexedDB就诞生了。它可以理解成浏览器提供的本地数据库，可储存大量数据，提供查找接口，建立索引，它更接近NoSQL数据库。特点如下：
+ 键值对储存
+ 异步操作：然后localStorage是同步操作的。
+ 支持事务：意味着操作中，有一步失败，则整个事务都被取消了，且回滚到事务发生之前。
+ 同源限制
+ 储存空间大：不少于250MB，且无上限。
+ 支持二进制储存

#### 2.基本概念
**2.1 数据库**
数据库是一系列相关数据的容器。每个域名都可以新建任意多个数据库。 
IndexedDB数据库有版本的概念。只可存在一个版本的数据库，若要修改数据库结构，则得通过升级数据库版本完成。

**2.2 对象仓库**
每个数据库包含若干个对象仓库。类似于关系数据库表格。

**2.3 数据记录**
每条记录类似于关系型数据库的行，每行只有主键和数据体两部分。主键需唯一；数据体不限格式。

**2.4 索引**
为了加速数据检索，为不同的属性建立了索引。

**2.5 事务**
数据记录的读写和删改，都是通过事务完成的。事务对象提供error、abort和complete三个事件，用来监听操作结果。

#### 3.操作流程
**3.1 打开数据库**
```
var request = window.indexedDB.open(databaseName, version);  //接受两个参数
```
indexedDB.open()方法返回IDBRequest对象。该对象通过三个事件error(失败)、success(成功)、upgradeneeded(数据库的升级)处理操作结果。   
```
//error事件
request.onerror = function(event){
    console.log('数据库打开错误')
}

//success事件
var bd;
request.onsuccess = function(event){
    db = request.result;   //通过request对象的srsult属性拿到数据库对象
    console.log('数据库打开成功')
}

//upgradeneeded事件
var db;
request.onupgradeneeded = function(event){
    db = event.target.result;
}
```

**3.2 新建数据库**
```
//第一步：新建对象仓库
request.onupgradeneeded = function(event){
    db = event.target.result;
    var objectStore = db.createObjectStore('person',{keyPath:'id'})
}
```

**3.3 新增数据**
通过事务可以完成向对象仓库写入数据记录。
```
function add(){
    var request = db.transaction(['person'], 'readwrite')
    .objectStore('person')
    .add({ id:1, name:'张三'，age:24, email:'zhangsan@example.com'});
}

request.onsuccess = function (event) {
console.log('数据写入成功');
};

request.onerror = function (event) {
console.log('数据写入失败');
}
```

**3.4 读取数据**
```
function read(){
    var transaction = db.transaction(['person']);
    var objectStore = transaction.objectStore('person');
    var request = objectStore.get(1);
}

request.onerror = function(event) {
 console.log('事务失败');
};

request.onsuccess = function( event) {
  if (request.result) {
    console.log('Name: ' + request.result.name);
    console.log('Age: ' + request.result.age);
    console.log('Email: ' + request.result.email);
  } else {
    console.log('未获得数据记录');
  }
};
```

**3.5 遍历数据**
使用指针对象IDBCursor来遍历数据表格的所有记录。
```
function readAll(){
    var objectStore = db.transaction('person').objectStroe('person')
    
    objectStore.openCursor().onsuccess = function(event){
        var cursor = event.target.result;
        
        if (cursor) {
           console.log('Id: ' + cursor.key);
           console.log('Name: ' + cursor.value.name);
           console.log('Age: ' + cursor.value.age);
           console.log('Email: ' + cursor.value.email);
           cursor.continue();
        } else {
          console.log('没有更多数据了！');
        }
        
    }
}
readAll();
```

**3.6 更新数据**
使用IDBObject.put()方法
```
function update(){
    var request = db.transaction(['person'], 'readwrite')
    .objectStore('person')
    .put({ id:1, name:'李四', age:35, email:'lisi@example.com'});
    
    request.onsuccess = function (event) {
        console.log('数据更新成功');
    };
    
    request.onerror = function (event) {
        console.log('数据更新失败');
    }
}
```

**3.7 删除数据**
IDBObjectStore.delete()方法用于删除记录。
```
function remove(){
    var request = db.transaction(['person'], 'readwrite')
        .objectStore('person')
        .delete(1);
    request.onsuccess = function(event){
        console.log('数据删除成功')
    }
}
remove();
```
**3.8 使用索引**
索引的意义在于，可以搜索任意字段。若不建立索引，默认就只能搜索主键。


#### 4.indexedDB对象    
浏览器原生提供indexedDB对象，作为开发者的操作接口。
**4.1 indexedDB.open()**   
用于打开数据库，是异步的操作。
```
var openRequest = window.indexedDB.open('test', 1);
```

## 未完待续 2019/9/6

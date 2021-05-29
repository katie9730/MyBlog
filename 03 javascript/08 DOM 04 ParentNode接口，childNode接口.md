+ parentNode接口：表示当前节点是一个父节点，提供一些处理子节点的方法
+ childNode接口：表示当前节点是一个子节点，提供一些相关的方法
******
### 1.ParentNode接口
**1.1 ParentNode.children**    
返回一个HTMLCollection实例，成员是当前节点的所有元素子节点。该属性为只读。
```
for(var i=0; i < el.children.length; i++){
    //...
}
```
**1.2 ParentNode.firstElementChild**     
返回当前节点的第一个元素子节点。若没有，则返回null。
```
document.firstElementChild.nodeName
```
**1.3 ParentNode.lastElementChild**   
返回当前节点的最后一个元素子节点，若没有，则返回null。

**1.4 ParentNode.childElementCount**   
返回一个整数，表示当前节点的所有元素子节点的数目。若没有，则返回0.

**1.5 ParentNode.append(),ParentNode.prepend()**   
append:为当前节点追加一个或多个子节点，位置是最后一个元素子节点的后面。（可添加元素子节点也可添加文本子节点。）
prepend：与append一致，只是它是放在第一个元素子节点的前面。

### 2.ChildNode接口   
若一个节点有父节点，则会继承ChildNode接口。
** 2.1 childNode.remove()**   
用于从父节点移除当前节点。
```
el.remove()
```
**2.2 ChildNode.before(),ChildNode.after()**
+ before:用于在当前节点的前面，插入节点（元素节点、文本节点）。两个拥有相同的父节点。
+ after：用于在当前节点的后面插入节点，用法相同。

**2.3 ChildNode.replaceWith()** 使用参数节点，替换当前节点（元素节点、文本节点）。

## 完结 2019/6/20
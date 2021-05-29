### Node接口   
所有DOM节点对象都继承了Node接口，拥有一些共同的属性和方法。这个是DOM操作的基础。
******
#### 1.属性
**1.1 Node.prototype.nodeType**  
NodeType属性返回一个整数值，表示节点的类型。

+ 不同节点nodeType属性值对应不同的常量
    - 文档节点（document）：9，对应常量Node.DOCUMENT_NODE
    - 元素节点（element）：1，对应常量Node.ELEMENT_NODE
    - 属性节点（attr）：2，对应常量Node.ATTRIBUTE_NODE
    - 文本节点（text）：3，对应常量Node.TEXT_NODE
    - 文档片断节点（DocumentFragment）：11，对应常量Node.DOCUMENT_FRAGMENT_NODE
    - 文档类型节点（DocumentType）：10，对应常量Node.DOCUMENT_TYPE_NODE
    - 注释节点（Comment）：8，对应常量Node.COMMENT_NODE

**1.2 Node.prototype.nodeName**    
nodeName属性返回节点的名称。
```
//HTML代码如下
//<div id='d1'>Hello World</div>
var div = document.getElementById('d1')；
div.nodeName //'DIV'
```

**1.3 Node.prototype.nodeValue**    
返回一个字符串，表示当前节点本身的文本值，该属性可读写。只对文本节点（text）、注释节点（comment）、属性节点（attr）有效，且会返回nodeValue。对于其他的节点设置无效，且返回null。
```
// HTML 代码如下
// <div id="d1">hello world</div>
var div = document.getElementById('d1');
div.nodeValue  //null
div.firstChild.nodeValue //'hello world'
```
**1.4 Node.prototype.textContent**    
返回当前节点和它所有后代节点的文本内容。可读写。
```
// HTML 代码为
// <div id="divA">This is <span>some</span> text</div>
document.getElementById('divA').textContent
// this is some text
```
**1.5 Node.prototype.baseURI**
baseURL属性返回一个字符串，表示当前网页的绝对路径。浏览器根据这个属性，计算网页上的相对路径的URL。该属性为只读。
```
// 当前网页的网址为
// http://www.example.com/index.html
document.baseURI
// "http://www.example.com/index.html"
```

**1.6 Node.prototype.ownerDocument**    
返回当前节点所在的顶层文档对象，即document对象。

**1.7 Node.prototype.nextSibling**    
返回当前节点后面的第一个同级节点。如果当前节点没有同级节点，则返回null。
```
// HTML 代码如下
// <div id="d1">hello</div><div id="d2">world</div>
var d1 = document.getElementById('d1');
var d2 = document.getElementById('d2');
d1.nextSibling === d2 // true
```

**1.8 Node.prototype.previousSibling**    
返回当前节点前面的、距离最近的一个同级节点。如果没有，则返回null。
```
// HTML 代码如下
// <div id="d1">hello</div><div id="d2">world</div>
var d1 = document.getElementById('d1');
var d2 = document.getElementById('d2');
d2.previousSibling === d1 //true
```

**1.9 Node.prototype.parentNode**    
返回当前节点的父节点。对于一个节点来说，父节点只可能是三种类型：元素节点（element）、文档节点（document）和文档片段节点（documentfragment）。

**1.10 Node.prototype.parentElement**
返回当前节点的父元素节点。如果没有父节点或者父节点类型不是元素节点，则返回null。父节点只可能是三种类型：元素节点、文档节点（document）和文档片段节点

**1.11 Node.prototype.firstChile,Node.prototype.lastChild**
+ firstChild属性返回当前节点的第一个节点，若没有则返回null。
+ lastChild属性返回当前节点的最后一个子节点。若没有则返回null。

**1.12 Node.prototype.childNodes**
返回类似数组的对象，成员包括当前节点的所有子节点。
```
var children = document.querySelector('ul').childNodes;
```

**1.13 Node.prototype.isConnected**    
返回布尔值，表示当前节点是否在文档之中。
```
var test = document.createElement('p');
test.isConnected //false

document.body.appendChild(test);
test.isConnected //true
```

### 2.方法
**2.1Node.prototype.appendChild()**
appendChild()方法接收一个节点对象作为参数，将其作为最后一个子节点，插入当前节点。

**2.2 Node.prototype.hasChildNodes()**    
返回一个布尔值，表示当前节点是否有子节点，该方法结合了firstChild和nextsibling属性。

**2.3 Node.prototype.cloneNode()**
用于克隆一个节点。接受一个布尔值作为参数。

**2.4 Node.prototype.insertBefore()**    
用于将某个节点插入父节点内部的指定位置。

**2.5 Node.prototype.removeChild()**    
接受一个子节点作为参数，用于从当前节点移除该子节点。

**2.6 Node.prototype.replaceChild()**    
用于将一个新的节点，替换当前节点的某一个子节点。

**2.7 Node.prototype.contains()**   
返回一个布尔值，表示参数节点是否满足以下三个条件之一
+ 参数节点为当前节点
+ 参数节点为当前节点的子节点
+ 参数节点为当前节点的后代节点
```
document.body.contains(node)
```

**2.8 Node.prototype.compareDocumentPosition()**   
用法与contains完全一致。返回二进制，表示参数节点与当前节点的关系。

**2.9 Node.prototype.isEqualNode()，Node.prototype.isSameNode()**   
返回布尔值，用于检查两个节点是否相等。所谓相等的节点，指的是两个节点的类型相同、属性相同、子节点相同。

**2.10 Node.prototype.normalize()**   
用于清理当前节点内部的所有文本节点。去除空的文本节点，并且将毗邻的文本节点合并成一个，也就是说不存在空的文本节点，以及毗邻的文本节点。

**2.11 Node.prototype.getRootNode()**
返回当前节点所在的文档的根节点document，与ownerDocument属性的作用相同。

## 完结 2019/6/20
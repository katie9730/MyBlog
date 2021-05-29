### 1.概述   
document节点对象代表整个文档，每张网页都有自己的document对象。window.document属性指向这个对象。 document对象有不同的办法可以获取
+ 正常网页：使用document或window.document。
+ iframe框架:使用iframe节点的contentDocument属性。
+ Ajax操作返回的文档:使用XMLHttpRequest对象的responseXML属性。
+ 内部节点：使用ownerDocument属性。

document对象继承了EventTarget接口，Node接口，ParentNode接口。

### 2.属性
**2.1快捷方式属性**    
指向文档内部的某个节点的快捷方式
+ 1):document.defaultView属性：返回document对象所属的window对象。若不属于,则返回null
+ 2):document.doctype属性：document对象一般有两个子节点，第一个子节点是document.doctype，指向<DOCTYPE>节点，即文档类型节点（DTD）。HTML的文档类型节点，一般写成<!DOCTYPE html>。若没有DTD，则返回null。
+ 3):document.documentElement属性：返回当前文档的根元素节点。通常是document节点的第二个子节点，即<html>节点。
+ 4):document.body,document.head属性
    - document.body属性指向<body>节点
    - document.head属性指向<head>节点
+ 5):document.scrollingElement属性：返回当前滚动元素
```
document.scrollingElement.scrollTop = 0;
```
+ 6.document.activeElement属性：返回获得当前焦点的DOM元素。通常返回<input>、<textarea>、<select>等表单元素。若没有焦点，则会返回<body>或者null。
+ 7.document.fullscreenElement属性：返回当前以全屏状态展示的DOM元素。如果没有，则返回null。


**2.2 节点集合属性**    
返回HTMLCollection实例，表示文档内部特定元素的集合。这些集合都是动态的，原节点有任何变化，立刻回反映在集合中。
+ 1):document.links属性：返回当前文档所有设定了href属性的<a>及<area>节点。
+ 2):document.forms属性：返回<form>表单节点。
+ 3):document.images属性：返回页面所有<img>图片节点。
```
var imglist = document.images;
for(var i=0, i<imglist.length; i++){
    if(imglist[i].src ==='banner.gif'){
        //...
    }
}
```
+ 4):document.embeds, document.plugins:都返回所有<embed>节点。
+ 5):document.scripts属性：返回所有<script>节点。
```
var scripts = document.scripts;
if (scripts.length !== 0){
    console.log('当前网页有脚本')；
}
```
+ 6):document.styleSheets属性:返回文档内嵌或引入的样式表集合。
+ 7):小结    
除了document.styleSheets，以上的集合属性返回的都是HTMLCollection实例。
```
document.links instanceof HTMLCollection //true
document.images instanceof HTMLCollection // true
document.forms instanceof HTMLCollection // true
document.embeds instanceof HTMLCollection // true
document.scripts instanceof HTMLCollection // true
```
HTMLCollection实例是类似数组对象，所以这些属性都有length属性，都可以使用方括号来引用成员。如果成员有id或name属性，还可以用这两个属性的值。

**2.3 文档静态信息属性**
+ 1):document.documentURI,document.URL   
    - 相同点：都返回一个字符串，表示当前文档的地址。
    - 不同点：继承不同的接口。documentURI继承Document接口,可用于所有文档。URL继承自HTMLDocument接口，只能用于HTML文档。
    - 如果文档的（#anchor）变化，这两个属性都会跟着变化。
+ 2):document.domain属性：返回当前文档的域名，不包含协议和接口。是只读属性。另外，设置document.domain会导致端口被改成null。因此，如果通过设置document.domain来进行通信，双方网页都必须设置这个值，才能保证端口相同。
+ 3):document.location:Location对象是浏览器提供的原生对象，提供URL相关的信息和操作方法。通过window.location和document.location属性，可以拿到这个对象。
+ 4):document.lastModified:返回一个字符串，表示当前文档最后修改的时间。
+ 5):document.title:返回当前文档的标题。此值可被修改。
+ 6):document.characterSet:返回当前文档的编码，例如UTF-8。
+ 7):document.referrer:返回一个字符串，表示当前文档的访问者来自哪里。
+ 8):document.dir:返回一个字符串，表示文字方向。rtl表示文字从右到左；ltr表示文字从左到右。
+ 9):document.compatMode:返回浏览器处理文档的模式，BackCompat（向后兼容模式）和CSS1Compat（严格模式）
**2.4 文档状态属性**
+ 1):document.hidden:返回布尔值，表示当前页面是否可见。
+ 2):document.visibilityState:返回文档的可见状态。
    - visible；页面可见
    - hidden：页面不可见
    - prerender：页面正处于渲染状态
    - unloaded：页面从内存里面卸载了
+ 3):document.readyState:返回当前文档的状态
    - loading：加载HTML代码阶段
    - interactive：加载外部资源阶段
    - complete：加载完成
    > 浏览器开始解析 HTML 文档，document.readyState属性等于loading。
浏览器遇到 HTML 文档中的<script>元素，并且没有async或defer属性，就暂停解析，开始执行脚本，这时document.readyState属性还是等于loading。
HTML 文档解析完成，document.readyState属性变成interactive。
浏览器等待图片、样式表、字体文件等外部资源加载完成，一旦全部加载完成，document.readyState属性变成complete。

**2.5 document.cookie**    
用来操作浏览器Cookie的，详见《浏览器模型》部分的《Cookie》章节。

**2.6 document.designMode**    
控制当前文档是否可编辑。该属性有两个值on和off(默认值)。为on时，就可编辑了。

**2.7 document.implementation**   
返回一个DOMImplementation对象。该对象有三个方法，主要用于创建独立于当前文档的新的Document对象。
+ DOMImplementation.createDocument()：创建一个XML文档。
+ DOMImplementation.createHTMLDocument():创建一个HTML文档。
+ DOMImplementation.createDocumentType()：创建一个DocumentType对象。


#### 3.方法
**3.1 document.open()，document.close()**
+ document.open方法：清除当前文档所有内容，使得文档处于可写状态。
+ document.close方法：用来关闭document.open()打开的文档。

**3.2 document.write(),document.writeIn()**
+ document.write方法：用于向当前文档写入内容。且当作HTML代码解析，不会转义。
+ 


## 未完待续 2019/6/22
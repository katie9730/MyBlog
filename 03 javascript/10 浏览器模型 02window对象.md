#### 1.概述
window对象指当前的浏览器窗口。即当前页面的顶层对象，所有对象都为他的下属。未声明就赋值的变量就会自动变成window对象的属性，它存在的弊端是使得编译阶段无法检测出未声明变量。

#### 2.window对象的属性
**2.1 window.name**    
字符串，表浏览器窗口的名字。主要用于配合超链接和表单的target属性的使用。    
**2.2 window.closed，window.opener**    
+ window.closed属性返回一个布尔值，表示脚本打开的新窗口是否关闭。
+ window.opener属性，表示打开当前窗口的父窗口。若没有父窗口，则返回null。

**2.3 window.self，window.window**    
两个都指向窗口本身，且都为只读。    

**2.4 window.frames，window.length**    
+ window.frames：返回一个类似数组的对象。成员为页面内所有框架的窗口，包括frame元素和iframe元素。frames属性实际上是window对象的别名。
+ window.length：返回当前网页包含的框架总数，若当前不包含frame和iframe元素，则window.length就返回0。 
+ 
**2.5 window.frameElement**    
主要用于当前窗口嵌在另一个网页的情况。返回当前网页所在的那个元素节点。若当前窗口不是顶层窗口，或者嵌入的那个网页不是同源的，则该属性返回null。    

**2.6 window.top，window.parent**    
+ window.top属性指向最顶层窗口，用于框架窗口里面获取顶层窗口。
+ window.parent属性指向父窗口，如果当前窗口没有父窗口，则window.parent指向本身。    
```
if (window.parent !== window.top){
    //表明当前窗口嵌入不止一层
}
```

**2.7 window.status**
用于读写浏览器状态栏的文本。不过很多浏览器不允许改写，所以此方法不一定有效。

**2.8 window.devicePixelRatio**
返回数值，表示一个css像素的大小与一个物理像素大小之间的比率

**2.9 位置大小属性**
+ window.screenX,window.screenY:返回浏览器窗口左上角相对于当前屏幕左上角的水平距离和垂直距离（单位像素）。只读。
+ window.innerHeight,window.innerWidth:返回网页在当前窗口中可见部分的高度和宽度。只读。
+ window.outerHeight,window.outerWidth:返回浏览器窗口的高度和宽度，包括浏览器菜单和边框。只读。
+ window.pageXOffset,window.pageYOffset:是window.scrollX和window.scrollY人别名。

**2.10 组件属性**
返回浏览器的组件对象
+ window.locationbar:地址栏对象
+ window.menubar:菜单栏对象
+ window.scrollbars:窗口的滚动条对象
+ window.toolbar:工具栏对象
+ window.statusbar:状态栏对象
+ window.personalbar:用户安装的个人工具栏对象

**2.11 全局对象属性**
+ window.document:指向document
+ window.location:指向location
+ window.navigator:指向navigator
+ window.history:指向history
+ window.localStorage:指向localStorage
+ window.sessionStorage:指向sessionStorage
+ window.console:指向console
+ window.screen:指向screen

**2.12 window.isSecureContext**
返回布尔值。表当前窗口是否处在加密环境。为HTTPS协议，则为true，否则为false。

#### 3.window对象的方法
**3.1 window.alert(),window.prompt(),window.confirm()**
都为浏览器与用户互动的全局方法。
+ window.alert()：弹出对话框，只有一个确定按钮，用来通知用户某些信息。
+ window.prompt()：弹出对话框，有个输入框，用于用户输入信息，用来获取用户输入的数据。
+ window.confirm()：弹出对话框，用于询问，有确认取消按钮。

**3.2 window.open()，window.close(),window.stop()**
+ window.open():用于新建另一个浏览器窗口，无法新建则返回null。接受三个参数。
    - url：字符串，表示新窗口的网址
    - windowName：字符串，表示新窗口的名字
    - windowFeatures:字符串，内容为逗号分隔的键值对。
+ window.colse():用于关闭当前窗口，
+ window.stop():等同于单击浏览器的停止按钮。

**3.3 window.moveTo(),window.moveBy()**
+ window.moveTo()：用于移动浏览器窗口到指定位置。接受两个参数，窗口左上角距离屏幕左上角的水平距离和垂直距离，单位px。
+ window.moveBy()：移动到一个相对位置，接受两个参数，分布是窗口左上角向右移动的水平距离和向下移动的垂直距离。单位px。

**3.4 window.resizeTo(), window.resizeBy()**
+ window.resizeTo()：用于缩放窗口到指定大小。接受两个参数，缩放后的窗口宽度outerWidth和缩放后的窗口高度outerHeight
+ window.resizeBy()：用于缩放窗口，与window.resizeTo()的区别在于它是按照相对的量缩放的。

## 未完待续 2019/9/6
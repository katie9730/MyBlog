## Navigator 对象
指向一个包含浏览器肯系统信息在Navigator对象。

### 1.1 Naviagtor对象的属性
+ Navigator.userAgent：返回浏览器User Agent，表示浏览器的厂商和版本信息。
+ Navigator.plugins：返回一个包含plugin实例对象的数组，表示浏览器安装胡插件。
+ Navigator.platform：返回用户操作系统信息。
+ Navigator.onLine：返回布尔值，表示用户当前是在线还是离线(浏览器断线)。在线触发online事件，离线触发offline事件。(歧义：浏览器)
+ Navigator.language：返回字符串，表示浏览器的首选语言(只读)。
+ Navigator.languages：返回数组，表示可以接受的语言。
+ Navigator.geolocation：返回Geolocation对象，包含用户地理位置的信息(只在HTTPS下可用)。
    - Geolocation.getCurrentPosition()：得到用户的当前位置
    - Geolocation.watchPosition()：监听用户位置变化
    - Geolocation.clearWatch()：取消`watchPosition()`方法指定的监听函数
+ Navigator.cookieEnabled：返回布尔值，表示浏览器的Cookie功能是否打开。

### 1.2 Navigator对象的方法
+ Navigator.javaEnabled()：返回布尔值，表示浏览器是否能运行Java Applet小程序
+ Navigator.sendBeacon()：用于向服务器异步发送数据

### 2.1 Scrren对象
表示当前窗口所在的屏幕，提供显示设备的信息。
+ Screen.height：浏览器窗口所在屏幕的高度
+ Screen.width：浏览器窗口所在的屏幕的宽度
+ Screen.awailHeight：浏览器窗口可用的屏幕高度
+ Screen.availWidth：浏览器窗口可用的屏幕宽度
+ Screen.pixelDepth：整数，表示屏幕的色彩位数。
+ Screen.colorDepth：应用程序的颜色深度
+ Screen.pixelDepth：屏幕的颜色深度
+ Screen.orientation：返回对象，表示屏幕的方向。type属性是一个字符串，表示屏幕的具体方向
    - landscape-primary：横放
    - landscape-secondary：颠倒的横放
    - portrait-primary：竖放
    - portrait-secondary：颠倒的竖放

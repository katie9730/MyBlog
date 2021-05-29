#### 1.概述   
Cookie是服务器保存在浏览器的一小段文本信息，每个Cookie的大小一般不超过4KB。浏览器每次向服务器发出请求，就会自动附上这段代码。    
Cookie主要用于分辨两个请求是否来自同一个浏览器，以及保存一些状态信息。常用场景如下：
+ 对话管理(session)：保存登录、购物车等需要记录的信息。
+ 个性化：保存用户的偏好。
+ 追踪：记录和分析用户行为。    

Cookie不推荐作为客户端储存。因为他的设计目标并不是这个，它容量小，缺乏数据操作接口，影响性能。客户端储存推荐使用Web storage API和IndexedDB。    

Cookie包含以下几方面信息
+ Cookie名字
+ Cookie的值
+ 到期时间
+ 所属域名（默认为当前域名）
+ 生效路径（默认为当前网址）

```
//浏览器是否打开Cookie功能
window.navigator.cookieEnabled
//document.cookie属性返回当前网页的cookie
document.cookie
```    
浏览器的同源政策规定，两个网址只要域名相同和端口相同，就可以共享Cookie（不要求协议相同）。

#### 2.Cookie与HTTP协议   
Cookie由HTTP协议生成，也主要供HTTP协议使用。

**2.1 HTTP回应：Cookie的生成**   
服务器如果希望在浏览器保存Cookie，就要在HTTP回应的头信息里面，放置一个set-Cookie字段
```
Set-Cookie:foo=bar
//浏览器保存一个名为foo的Cookie，它的值为bar。
```
**2.2 HTTP请求：Cookie的发送**    
浏览器向服务器发送HTTP请求时，每个请求都会带上相应的Cookie。也就是说，把服务器早前保存在浏览器的这段信息，再发回服务器。这时要使用HTTP头信息的Cookie字段。
```
Cookie:foo=bar
//这段代码会向服务器发送名为foo的Cookie，值为bar。
```
   
服务器收到浏览器发来的Cookie时，有两点是未知的
+ Cookie的各种属性，比如何时过期
+ 哪个域名设置的Cookie，到底是一级还是二级域名？


#### 3.Cookie属性
**3.1 Expires，Max-Age**
+ Expires:指定一个具体到期时间，到了指定时间后，浏览器不再保存这个Cookie。若这个值为null，则会话关闭，内容则被删除。
+ Max-Age：从现在开始Cookie存在的秒数。过了这个时间以后，浏览器就不再保存这个Cookie了。与Expires相比，它具有优先生效权。    
若两个属性都没有，那么这个Cookie就是Session Cookie，即它只在本次对话存在，一旦关闭浏览器就不会保留这个了。   

**3.2 Domain，path**
+ Domain属性：指定浏览器发出HTTP请求，那些域名要附带这个Cookie。若没有指定该属性，浏览器默认将其设为当前域名，这是子域名将不会附带这个Cookie。
+ path属性：指定浏览器发出HTTP请求时，那些路径要附带这个Cookie。

**3.3 Secure，HttpOnly**
+ Secure属性：指定浏览器只有在加密协议HTTPS下，才能将这个Cookie发送给服务器。另一方面，如果当前协议是HTTP，浏览器会自动忽略服务器发来的Secure属性。
+ HttpOnly属性：指定该Cookie无法通过JavaScript脚本拿到，主要是document.cookie属性、XMLHttpRequest对象和Request API都拿不到该属性。

**4. document.cookie**    
用于读写当前网页的Cookie。读取的时候，他会返回当前网页的所有cookie，前提是该Cookie不能有HTTPOnly属性。

**5. Chrome 51新增SameSite属性**  [摘自](http://www.ruanyifeng.com/blog/2019/09/cookie-samesite.html)     
该属性主要用来防止CSRF攻击和用户追踪的,从而减少安全风险。    
> 什么是CSRF攻击？    
Cookie往往用来存储用户的身份信息，恶意网站可以设法伪造带有正确Cookie的HTTP请求，这就是CSRF攻击。利用第三方网站引导发出的Cookie，就称为第三方Cookie。他除了CSRF攻击，还可以用于用户追踪。    

SameSite属性的三个值
+ Strict(最为严格)：完全禁止第三方Cookie，跨站点是，任何情况下都不会发送Cookie。换言之，只有当前网页的URL与请求目标一致，才会带上Cookie。由于这个规则过于严格，可能会造成不好的用户体验。
`Set-Cookie:CookieName=CookieValue; SameSite=Strict；`
+ Lax：规则稍稍放宽，大多数情况也是不会发送第三方Cookie，但是导航到目标网址的Get请求除外。
`Set-Cookie: CookieName=CookieValue; SameSite=Lax;`
设置了Strict或Lax以后，基本可以杜绝CSRF攻击。
```
请求类型	    示例	                             正常情况	    Lax
链接	    <a href="..."></a>	                 发送 Cookie	发送 Cookie
预加载   	<link rel="prerender" href="..."/>	 发送 Cookie	发送 Cookie
GET 表单	<form method="GET" action="..."> 	 发送 Cookie	发送 Cookie
POST 表单	<form method="POST" action="...">	 发送 Cookie	不发送
iframe	    <iframe src="..."></iframe>	         发送 Cookie	不发送
AJAX	    $.get("...")	                     发送 Cookie	不发送
Image	    <img src="...">	                     发送 Cookie	不发送
```
+ None：chrome计划将Lax变为默认设置。这时，网站可以选择显式关闭SameSite属性，将其设为None。不过，前提是必须同时设置Secure属性（Cookie 只能通过 HTTPS 协议发送），否则无效。
```
无效
Set-Cookie: widget_session=abc123; SameSite=None

有效
Set-Cookie:widget_session=abc123; SameSite=None; Secure

```

## 完结 2019/9/5
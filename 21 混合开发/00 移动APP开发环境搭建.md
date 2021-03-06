#### 前端混合App开发框架
1. Html5+、ReactNative、Weex、Ionic
2. [认识HTML5+](http://www.html5plus.org/#home)
 + h5+是一个产业联盟，它有一些互联网成员，专门在中国推广H5
3. [HBuilder官网](http://www.dcloud.io/)

#### 使用HBuilder生成安卓应用（在线）
[API地址](http://www.html5plus.org/doc/zh_cn/webview.html)     
Hbuilder是一个在线打包工具，不需要在本地配置开发环境，而是直接将做好的网站，通过一些简单的操作，在线打包一个App出来。
+ 在项目上右键->发行->发行为原生安装包
+ 好处：本地不用配置开发环境；操作方便；对于程序员来说，无需关心打包过程且是透明的。
+ 缺点：程序员难干预打包过程，源代码提交到云端服务器，存在项目核心代码被泄露的风险。

#### 介绍H5+和RN这两种APP开发技术
**使用H5+ 或者Ionic进行移动APP开发**
+ 首先制作一个完整的网站，其中在网站的基础上，使用H5+或Ionic提供打包技术，将网站打包成一个应用。目的是为了能够安装到手机上和调用硬件底层的API。打包完成，就得到一个安卓的应用。应用内部就是其实就是一个网站。
> 好处：开发效率高。     
> 缺点：内部本质上是一个网站，运行效率和性能不太好。

**使用ReacNative或Weex进行移动APP开发**
+ 首先开发一个完整的项目，只不过不是网站，而是模板项目。所以它不能运行到浏览器中，也不能运行在手机中的一个半成品。使用RN或Weex提供的打包命令行。将模板项目中的源代码逐行翻译成原生的Java或OC代码。这种方式是使用前端技术开发出来的拥有原生性质的APP。
> 好处：运行性能高于前者，体验流畅      
> 缺点：可用的组件没有左侧的多

## 未完待续
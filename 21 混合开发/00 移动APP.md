## 移动APP第一天

#### 什么是混合移动App开发【重点】
1. 移动端开发分为安卓端开发、IOS端开发和混合移动APP开发技术三种。
2. 混合移动App开发技术，并没有使用苹果或安卓官方推荐的开发平台和开发方式，而是抛弃了官方提供的方式，使用前端独有的技术进行移动APP开发体验。
> 什么是移动App开发：通俗的理解，就是开发Web网站的技术（HTML+CSS+JS），通过某种方式，移植到移动App开发上进行使用，这种利用web开发技术进行移动端开发体验的方式，叫做混合移动APP开发！

#### 移动开发的几个概念
+ 原生开发（NativeApp）：指使用IOS、Android官方提供的工具，开发平台、配套语言进行的手机APP开发方式
+ 混合开发（HybirdApp）：使用前端已有的技术（HTML+CSS+JS），然后再搭配一些相关的打包编译技术，就能够开发出一个手机APP，安装到手机中进行使用。
+ APP的分类
    - 按照平台来划分
        * pc端
        * 移动端
        * 电视
    - 按照功能来划分
        * 游戏
        * 应用
+ App和web的区别
    - App的概念（Application）：可安装的应用程序。
        * 优点：流畅、稳定、基本上一些APP都可以运行，用户体验好。
        * 缺点：不能跨平台
    - Web概念：特指基于浏览器的web网站（本质就是网页）
        * 优点：可以跨平台（浏览器天生就是跨平台的）
        * 缺点：没有APP流畅、不稳定、受限于网速。
        
#### 市面上常见的App开发方式
+ webApp：基于浏览器实现的，有特定功能的网站，称作webapp
    - 优点：跨平台
    - 缺点：依赖网络，有白屏效果，相对来说，用户体验差；不能调用硬件底层的设备，比如摄像头
+ NativeApp:用Android和object-c等原生语言开发的应用
    - 优点：体验好；用户使用起来很流畅；非常适合做游戏【性能】；可以直接调用硬件底层的API；
    - 缺点：不能跨平台
+ HybirdApp：利用前端所学的知识去开发移动端App，兼具两者的优势。
    - 优点：能够跨平台；体验会好一些。
    - 缺点：相对于原生体验稍微弱一点，不适合做游戏
+ 注意：使用Java或者IOS写出来的代码和程序，在最终运行的时候，普通的文本代码，都会被编译为原生的机器码去运行，并不像js这样，解析执行，Java代码是编译执行。

#### 企业如何选择适合自己的APP开发方式
+ 游戏级别的使用原生开发。
+ 应用级别的使用混合APP开发。

#### 企业中项目开发流程
+ 需求调研：产品定位、受众群体、开发价值；【产出物：需求文档】
+ 产品设计：功能模块、流程逻辑；【产出物：设计文档，交互稿】，确定项目的基本功能；
+ 项目开发：项目架构、美工、前端、后台、测试【产品的把控】**理解前后端的概念**
+ 运营维护：上线试运行、调bug、微调功能模块、产品迭代

#### 企业技术选型 - 几大主流技术之间的关系
1. Angular.js 和 Ionic
 + [Angular1官网](https://angularjs.org/)
 + [Angular2官网](https://angular.io/)
 + [Ionic 中文网](http://www.ionic.wang/)
 + [Ionic 英文官网](http://ionicframework.com/getting-started/)
2. Vue.js 和 Weex
 + [Vue.js官网](https://cn.vuejs.org/)
 + [Weex文档](http://weex.apache.org/cn/references/index.html)
 + [Weex - github地址 - 新](https://github.com/apache/incubator-weex)
 + [Weex - github地址 - 旧](https://github.com/alibaba/weex)
3. React.js 和 React-Native
 + [React.js英文官网](https://facebook.github.io/react/)
 + [ReactNative中文网](http://reactnative.cn/)
 + [ReactNative英文网](http://facebook.github.io/react-native/)
 
> Angular,Vue,React这三个都是前端框架，我们在进行混合App开发的时候，只是用到了这三个框架的【基础语法】而已；
> Ionic,Weex,ReactNative这三个都是打包工具（提供了相关的命令行，只是运行指定的命令，就能够把项目打包成一个手机App出来），能够把我们开发出来的应用，直接打包成一个可安装的手机端程序安装包；同时，这三个东西，也提供了好用的一些小组件，方便我们去构建移动App的用户界面。

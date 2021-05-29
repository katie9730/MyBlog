***vue概述***     
>是一套构建用户界面的渐进式框架。 
>>特点
>> * 核心只关注视图层
>> * 易学，轻量，灵活的特点
>> * 适用于移动端项目
>> * 渐进式框架

***框架和库***
* 框架（vue：拥有完整的解决方案。我们写好人家调用我）
* 库（jquery、underscore、zepto、animate.css 我们调用它）

***渐进式（渐进增强）***
* vue全家桶 vuejs + vue-router（单页应用）+ vuex（组件化开发） + axios（获取数据 ）
* 通过组合 完成一个完整的框架

***渐进式理解*** 
* 声明式渲染
* 组件系统
* 客户端路由（vue-router）
* 大规模状态管理（vuex）
* 构建工具（vue-cli）

***vue的两大核心点***
* 响应的数据变化（当数据发生变化->视图的自动更新）
* 组合的视图组件（ui页面映射为组件树，划分组件可维护、可复用、可测试）

***Node(后端)中的MVC与前端中的MVVM之间的区别***
+ MVVM模式（angular，vue，React）双向：是前端视图层的概念，主要是视图层分离
    - model数据
    - view视图
    - viewModel视图模型:是model与view之间的调度者

+ MVC模式(backbone) 单向：是后端分层开发的概念
    - model数据
    - view视图
    - controller 控制器

***安装vue***
* cdn方式
* npm安装(node package manager)
> * npm init:初始化会产生一个package.json的文件，这个文件用来描述项目的依赖，项目名称不能有大写、特殊字符、中文，而且不要和安装的包的名字相同。
* 【MIT】指的是开源协议

***vue不支持ie8以下版本***
因为ES5中的Object.defineProperty没有替代方案



***vue第一天复习***
- vm => viewModel 数据最终都会被vm所代理
- {{a}}取值表达式，通过{{}}来进行取值，默认可以不写this，表达式 赋值运算 计算 三元表达式,尽量少写逻辑(computed)
- 事件v-on(@)  
   - 绑定给dom元素，函数需要定义在methods中，不能和data里的内容重名，this指向的是实例，不能使用箭头函数，事件源对象如果不写括号，可以自动传入，否则只能手动传入$event。
   ```
  <div @事件名="fn"></div>
   ```
 

***安装***    
npm install vue axios bootstrap
#### React技术栈
- react：UI渲染
- redux：管理数据
- react-router：管理路由
- webpack：配置工程
- ES6：代码优雅
- redux-saga：处理异步请求
- reselect：用来减少state改变带来的渲染压力

#### 页面初始化渲染过程
- 解析HTML，开始构建DOM树
- 解析css，生成css规则树
- 合并DOM树和css规则树，生产render树
- 布局render树，属于js中回流过程
- 绘制render树，属于重绘的过程
- 浏览器会把各层的信息发送给GPU(图像处理器)，GPU将各层合成(composite)，显示在屏幕上。

#### v-dom的缺点
ReactJS使用虚拟DOM机制，让前端开发者为每个组件提供一个render函数。render函数把props和state转换成ReactJS的虚拟DOM，然后ReactJS框架根据render返回虚拟DOM创建相同结构的真实DOM。每当state更改时，ReactJS框架重新调render函数。然后，框架会比较上次生产的虚拟DOM和新的虚拟DOM有哪些差异，进而把差异应用到真实DOM上。如此会存在以下两个缺点
- 即使state的改动再小，render也会完整的计算一遍，如果render函数较复杂，这个过程就会很浪费资源
- ReactJS框架比较虚拟DOM差异的过程，即慢又容易出错。

#### diff算法
当组件更新的时候，react会创建一个新的虚拟dom树并且会和之前储存的dom树进行比较的过程。初始化的时候倒是用不到。

#### 组件生命周期
##### 组件初始化会触发的5个钩子函数
- getDefaultProps():设置默认的props，相当于ES6中的static defaultProps = {}
- componentWillMount():组件初始化时调用，整个生命周期只调用一次。
- render():React最重要的步骤，创建虚拟dom，进行diff算法，更新dom树
- componentDidMount():进入状态后的调用，组件一般初始化都在这里请求。

##### 组件交互更新时触发的5个勾子函数
- componentWillReceiveProps(nextProps):组件初始化不调用，组件接受新的props时调用。
- shouldComponentUpdate(nextProps, nextState):性能优化的重要一环。组件接受新的state或者props时调用，设置在此对比前后两个props和state是否相同。如果相同就返回false阻止更新。
- componentWillUpdate(nextProps, nextState):组件初始化时不调用，只在组件将要更新时才调用。
- render()
- componentDidUpdate():组件初始化时不调用，组件更新完成后调用。

#### 组件卸载时调用
- componentWillUnmount():组件将要卸载时调用。

### react-router
Route可以像绑定的组件传递7个属性:children(以路由的包含关系为区分组件)、history、location(包含地址，参数，地址切换方式，key值，hash值)、params、route、routeParams、routes.

### 组件间的通信
- 父子之间传递：父级将一个回调函数当作属性传递给子级，子级可以直接调用函数与父级通信。
- 层级较深的通信：使用`getChildContext`来传递信息，通过`this.context`直接返访问，免去函数一层层往下传。
- 兄弟组件通信：建议使用redux。

### redux
进行逻辑运算、储存数据和实现组件尤其是顶层组件通信。
```
// redux的工作原理如下:
react-redux提供了connect和provider两个好基友，他们一个将组件与redux关联起来，一个将store传给组件。组件通过dispatch发出action，store根据action的type属性调用对应的reducer并传入state和这个action，reducer对state进行处理并返回一个新的state放入store。connect监听到store发生变化，调用setState更新组件，此时组件的props也就跟着变化了。
```
redux主要由三部分组成：store, reducer, action。
- store是一个对象，包含以下4个方法。
    + dispatch: 用于action的分发
    + subscribe：监听state的变化
    + getState：获取store中的state
    + replaceReducer：替换reducer，改变state修改的逻辑
- action：是一个对象，并且type属性是必须的，同时可以传入一些数据。action可以用actionCreator进行创造。dispatch就是把action对象发送出去。
- reducer：是一个函数。接受一个state和一个action。
- combineReducers：其实是一个reducer,接受整个state和一个action。
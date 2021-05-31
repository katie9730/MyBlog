## React面向组件编程
## 使用React开发者工具调试
- 翻墙情况下：在Google应用商店直接下载使用
- 未翻墙的情况下：
    + 下载离线`React Developer Tools`包
    + Google浏览器-设置-更多工具-扩展程序-加载已解压的扩展程序-选择`React Developer Tools`包

## 两种定义组件的方式
- 函数式组件：适用于【简单组件】的定义
- 类式组件：适用于【复杂组件】的定义
> 何为简单组件、复杂组件?没有状态(state)的组件称为简单组件; 有状态(state)的组件称为复杂组件

## 组件实例的三大核心属性
### 1) state
- 理解
    1.state是组件对象最重要的属性，值是对象(可以包含多个key-value)的组合
    2.组件被称为“状态机”，通过更新组件的state来更新对应的页面显示(重新渲染组件)
- 强烈注意
    1.组件中render方法中的this为组件实例对象
    2.组件定义的方法中this为undefined，如何解决？
        * 强制绑定this：通过函数对象的bind()
        * 箭头函数
    3.状态数据，不能直接修改或更新
### 1) props
- 理解
    1.每个组件对象都会有props(properties的简写)属性。
    2.组件标签的所有属性都保存在props中
- 作用
    1.通过标签属性从组件外向组件内传递变化的数据
    2.注意：组件内部不要修改props数据
- 编码操作
    1.内部读取某个属性值：`this.props.name`
    2.对props中的属性进行类型限制和必要性限制
        * 第一种方式（React v15.5 开始已弃用）
        ```
        Person.propTypes = {
            name: React.PropTypes.string.isRequired,
            age: React.PropTypes.number
        }
        ```
        * 第二种方式（新）
        ```
        // 使用prop-types库进行限制（需要引入prop-types库）
        Person.propTypes = {
            name: PropTypes.string.isRequired,
            age: PropTypes.number
        }
        ```
- 扩展属性：将对象的所有属性通过props传递。`<Person {...person}/>`
- 默认属性值
```
Person.defaultProps = {
    age: 18,
    sex: '男'
}
```
- 组件类的构造函数
```
constructor(props) {
    super(props)
    console.log(props) // 打印所有属性
}
```

### 1) refs与事件处理
- 关于refs的三种方式
    + string类型的方式`<input ref='input1'/>`
    + 回调函数的方式`<input ref={(c) => {this.input1 = c}} />`
        * 如果ref回调函数以内联函数的方式定义，在更新过程中它会执行两次，第一次传入参数null，第二次传入参数DOM元素。这是因为每次渲染时会创建一个新的函数实例，React先清空旧的ref再设置新的。不过通过ref的回调函数定义成calss所绑定的函数的方式，可以避免这个问题。不过这是无关紧要的，怎样写都成
    + creatRef API的方式(React推荐)
    ```
    myRef = React.createRef()
    <input ref={this.myRef} />
    ```

## constructor()
若不初始化state或不进行方法绑定，则不需要为React组件实现构造函数。通常，在React中，构造函数仅用于以下两种情况：
- 通过给this.state赋值对象来初始化内部state。不要在`constructor`函数中调用`setState()`方法。
- 为事件处理函数绑定实例

## 事件处理
- 通过onXxx属性指定事件处理函数（注意大小写）
    + React使用的是自定义(合成)事件，而不是使用原生的DOM事件。——————为了更好的兼容性
    + React中的事件是通过委托方式处理的（委托给组件最外层的元素）。——————为了高效
- 通过event.target得到发生事件的DOM元素对象。——————不要过度使用ref

## 受控组件(推荐)与非受控组件
受控组件是指数据直接维护到实例的state中，非受控组件则不会维护到实例的state中。（这个类似于Vue的数据双向绑定）

## 高阶函数
如果一个函数符合下面2个规范中的任何一个，那该函数就是高阶函数。
- 若A函数，接受的参数是一个函数，那么A就可以称之为高阶函数。
- 若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数。
> 常见的高阶函数有：promise、setTimeout、arr.map()等等

### 函数的柯里化
通过函数调用继续返回函数的方式，实现多次接受参数最后统一处理的函数编码形式。

## 生命周期
### 理解
- 组件从创建到死亡会经历一些特定的阶段。
- React组件中包含一系列钩子函数(生命周期回调函数),会在特定的时刻调用。
- 我们在定义组件时，会在特定的生命周期回调函数中做特定的工作。   

### 生命周期流程图（旧）
- 挂载阶段
    + constructor：构造器
    + componentWillMount：组件将要挂载的钩子
    + render：组件挂载中 ===> 必须使用
    + componentDidMount：组件挂载完毕的钩子 ===> 常用
        * 一般在这个钩子中做一些初始化的事，例如：开启定时器、发送网络请求、订阅消息
- 更新阶段
    + setState()更新流程
        * shouleCOmponentUpdate()
        * componentWillUpdate()
        * render()
        * componentDidUpdate()
    + forceUpdate()强制更新
        * shouldComponentUpdate()
        * componentWillUpdate()
        * render()
        * componentDidUpdate()
    + 父组件render
        * componentWillReceiveProps()：注意第一次接受props不调用
        * shouldComponentUpdate(): 是否可以更新的阀门
        * componentWillUpdate()
        * render()
        * componentDidUpdate()
- 销毁阶段
    + componentWillUnmount(): ===> 常用
        * 一般在这个钩子中做一些收尾的事，例如：关闭定hi器、取消订阅消息。

## 生命周期（新）
### 过时的生命周期
由于以下生命周期方法经常被误解和滥用。考虑这三个生命周期在以后版本发布的异步渲染功能中可能潜在的误用问题更大。所以在17版本（包含17版本）后的版本中为这些生命周期添加“UNSAFE_”前缀。（这里的“unsafe”不是指不安全性，而是指使用这些生命周期的代码在React的未来版本中可能出现bug，尤其是启用异步渲染之后。）
- componentWillMount()
- componentWillUpdate()
- componentWillReceiveProps()

### 新增的生命周期
- getDerivedStateFromProps():在调用render方法之前调用，并且在初始挂载及后续更新时都会被调用。返回一个对象来更新state，如果返回null则不更新任何内容。
- getSnapshotBeforeUpdate():在最近的一次渲染输出之前调用。它使得组件在发生更改之前从DOM中捕获一些信息。此生命周期的任何返回值将作为参数传递给`componentDidUpdate()`

### 生命周期流程图（新）
- 挂载时
    + constructor()
    + getDerivedStateFromProps()
    + render()
    + componentDidMount() ===> 常用
        * 一般在这个钩子中做一些初始化的事，例如：开启定时器、发送网络请求、订阅消息
- 更新时
    + New props
        * getDerivedStateFromProps()
        * shouldComponentUpdate()
        * render()
        * getSnapshotBeforeUpdate()
        * ComponentDidUpdate
    + setState()
        * getDerivedStateFromProps()
        * shouldComponentUpdate()
        * render()
        * getSnapshotBeforeUpdate()
        * componentDidUpdate()
    + forceUpdate()
        * getDerivedStateFromProps()
        * render()
        * getSnapshotBeforeUpdate()
        * componentDidMount()
- 卸载时
    + componentWillUnmount() ===> 常用
        * 一般在这个钩子中做一些收尾的事，例如：关闭定hi器、取消订阅消息。

## 重要的钩子
- render: 初始化渲染或更新渲染调用
- componentDidMount: 开启监听，发送ajax请求
- componentwillUnmount: 做一些收尾工作，如清理定时器


## 经典面试题系列
```
	/*
   经典面试题:
      1). react/vue中的key有什么作用？（key的内部原理是什么？）
      2). 为什么遍历列表时，key最好不要用index?
      
			1. 虚拟DOM中key的作用：
					1). 简单的说: key是虚拟DOM对象的标识, 在更新显示时key起着极其重要的作用。

					2). 详细的说: 当状态中的数据发生变化时，react会根据【新数据】生成【新的虚拟DOM】, 
												随后React进行【新虚拟DOM】与【旧虚拟DOM】的diff比较，比较规则如下：

									a. 旧虚拟DOM中找到了与新虚拟DOM相同的key：
												(1).若虚拟DOM中内容没变, 直接使用之前的真实DOM
												(2).若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM

									b. 旧虚拟DOM中未找到与新虚拟DOM相同的key
												根据数据创建新的真实DOM，随后渲染到到页面
									
			2. 用index作为key可能会引发的问题：
								1. 若对数据进行：逆序添加、逆序删除等破坏顺序操作:
												会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低。

								2. 如果结构中还包含输入类的DOM：
												会产生错误DOM更新 ==> 界面有问题。
												
								3. 注意！如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，
									仅用于渲染列表用于展示，使用index作为key是没有问题的。
					
			3. 开发中如何选择key?:
								1.最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值。
								2.如果确定只是简单的展示数据，用index也是可以的。
   */
	
	/* 
		慢动作回放----使用index索引值作为key

			初始数据：
					{id:1,name:'小张',age:18},
					{id:2,name:'小李',age:19},
			初始的虚拟DOM：
					<li key=0>小张---18<input type="text"/></li>
					<li key=1>小李---19<input type="text"/></li>

			更新后的数据：
					{id:3,name:'小王',age:20},
					{id:1,name:'小张',age:18},
					{id:2,name:'小李',age:19},
			更新数据后的虚拟DOM：
					<li key=0>小王---20<input type="text"/></li>
					<li key=1>小张---18<input type="text"/></li>
					<li key=2>小李---19<input type="text"/></li>

	-----------------------------------------------------------------

	慢动作回放----使用id唯一标识作为key

			初始数据：
					{id:1,name:'小张',age:18},
					{id:2,name:'小李',age:19},
			初始的虚拟DOM：
					<li key=1>小张---18<input type="text"/></li>
					<li key=2>小李---19<input type="text"/></li>

			更新后的数据：
					{id:3,name:'小王',age:20},
					{id:1,name:'小张',age:18},
					{id:2,name:'小李',age:19},
			更新数据后的虚拟DOM：
					<li key=3>小王---20<input type="text"/></li>
					<li key=1>小张---18<input type="text"/></li>
					<li key=2>小李---19<input type="text"/></li>


	 */
```
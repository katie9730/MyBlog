## 3.create-react-app 创建react应用
### 3.1.1 react脚手架
- xxx脚手架：用来帮助程序员快速创建一个基于xxx库的模板项目
    + 包含了所有需要的配置（语法检查、jsx编译、devServer）
    + 下载好了所有相关的依赖
    + 可以直接运行一个简单效果
- react提供了一个用于创建react项目的脚手架库：create-react-app
- 项目的整体技术架构为：react + webpack + es6 + eslint
- 使用脚手架开发的项目的特点：模块化、组件化、工程化

### 3.1.2 创建项目并启动
- 第一步：全局安装`npm install -g create-react-app`
- 第二步：切换到想要创建项目的目录，使用命令`create-react-app hello-react`
- 第三步：进入项目文件夹：`cd hello-react`
- 第四步：启动项目：`npm start`

```
- yarn eject: 将所有隐藏的webpack文件都暴露出来了，且不可逆。
```

#### 3.1.3 安装快捷键插件`ES7 React/Redux/GraphQL/React-Native snippets
`

#### 3.1.4 功能界面的组件化编码流程
- 拆分组件：拆分界面，抽取组件
- 实现静态组件：使用组件实现静态页面的效果
- 实现动态组件
    + 动态显示初始化数据
        * 数据类型
        * 数据名称
        * 保存在那个组件？
    + 交互(从绑定事件监听开始)

```
1. 绑定的值与获取的值为同一个元素，那么就不需要ref绑定，直接读取事件的event即可。
2. UUID 是 通用唯一识别码。可以用在随机生成的id上。缩小版可用nanoid。
3.prop-types定义类型以及必要性的限制
4.defalutChecked只针对第一次有效果
```

## 55 组件化编码流程 10:39
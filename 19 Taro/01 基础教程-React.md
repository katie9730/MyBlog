### 1.开始
Taro通过`import * as React from 'react'`来使用React。

### 2.入口文件
每个Taro应用都需要一个入口组件来注册应用，入口文件默认是`src`目录下的app.js,入口组件必须导出一个React组件，在入口组件中我们可以设置全局状态或访问小程序入口实例的生命周期。
```
[src/app.js]
import React, { Component } from 'react'
import { Provider } from 'react-redux' // 假设我们要使用Redux
import configStore from './store'
import './app.css'
const store = configStore()

class App extends Component{
    componentDidMount() {}
    componentDidShow() {} // 对应onShow
    componentDidHide() {} // 对应onHide
    componentDidCatchError() {} // 对应onError
    render() {
        return {
            <Provider store={store}>
                {this.props.children} /*this.props.children是将要被渲染的页面*/
            </Provider>
        }
    }
}
export default APP
```
```
[app.config.js]
export default {
    pages: [
        'pages/index/index'
    ],
    window: {
        backgroundTextStyle: 'light',
        navigationBarBackgroundColor: '#fff',
        navigationBarTitleText: 'WeChat',
        navigationBarTextStyle: 'black'
    }
}
```

### 3.组件生命周期
- onLaunch(options)：在此生命周期`getCurrentInstance().router.params`可以访问到程序初始化参数。
- componentWillMount：监听程序初始化，初始化完成时触发（全局只触发一次）
    + path:启动小程序的路径
    + scene:启动小程序场景值
    + query:启动小程序的query参数
    + shareTicket:详见获取更多转发信息
    + referrerInfo:来源信息。从另一个小程序、公众号或App进入小程序时返回（appId, extraData, sourceServiceId）。否则返回{}
- componentDidMount():页面初次渲染完成时触发，一个页面只会调用一次。此生命周期可以访问`getCurrentInstance().router`。此生命周期可以访问 Taro DOM 并且更改 DOM 或添加事件，但无法通过 Taro.createSelectorQuery 查找小程序 DOM。
- componentDidShow(options):程序启动，或从后台进入前台显示时触发。wx小程序可使用`Taro.onAppShow`绑定监听，此生命周期中通过`getCurrentInstance().router.params`,可以访问到程序初始化参数。
- componentDidHide():程序从前台进入后台时触发。wx小程序可使用`Taro.onAppHide`绑定监听
- componentDieCatchError(string error):程序发生脚本错误或API调用报错时触发。wx小程序可使用`Taro.onError`绑定监听。
- componentDidNotFound(object):程序要打开的页面不存在时触发，wx小程序可使用`Taro.onPageNotFound`绑定监听。

### 4.页面组件
#### 4.1配置文件
一个页面文件（`./pages/index/index.jsx`）对应一个页面配置文件(`./pages/index/index.config.js`)默认导出后就是页面配置。
#### 4.2生命周期（以下所有生命周期中，都可以通过getCurrentInstance().router.params获取当前页面路径参数）
- onReady():页面首次渲染完毕时执行。
- onLoad(options):页面创建时执行。
- componentWillMount():页面加载时触发，一个页面只会调用一次，此时页面DOM尚未准备好，还不能和视图层进行交互。
- componentDidMount():页面初次渲染完成时触发，且一个页面也只会调用一次。
- shouldComponentUpdate(nextProps, nextState):页面是否需要更新。
- componentWillUpdate(nextProps, nextState):页面即将更新。
- componentDidUpdate(prevProps, prevState):页面更新完毕。
- componentWillUnmount():页面卸载时触发，如redirectTo或navigateBack到其他页面时。
- componentDidShow(): 页面显示/切入前台时触发。
- componentDidHide(): 页面隐藏/切入后台时触发。如navigateTo或tab切换到其他页面，小程序切入后台等。

#### 4.3页面事件处理函数
在小程序中，页面中专属的事件处理函数。
- onPullDownRefresh():监听用户下拉刷新事件。通过`Taro.startPullDownRefresh`触发下拉，`Taro.stopPullDownRefresh`停止下拉刷新。
- onReachBottom():监听用户上拉触底事件。
- onPageScroll(object):监听用户滑动页面事件
- onShareAppMessage(Object):监听用户点击页面内转发按钮（Button组件openType=‘share’）或右上角菜单“转发按钮的行为，并自定义转发内容”。注意，只有定义了此事件处理函数，右上角菜单才会显示“转发”按钮
- onResize(Object):小程序屏幕旋转时触发。
- onTabItemTap(Object):点击tab时触发。
- onAddToFavorites(Object):监听用户点击右上角菜单“收藏”按钮的行为，并自定义收藏内容。
- onShareTimelind():监听右上角菜单“分享到朋友圈”按钮行为，并自定义分享内容。注意，只有定义了此事件处理函数，右上角菜单才会显示“分享到朋友圈”按钮。
- componentWillPreload():预加载钩子。
- onTitleClick():点击标题触发。
- onOptionMenuClick():点击导航栏额外图标触发。
- onPopMenuClick()
- onPullIntercept():下拉截断时触发。
> 页面事件函数各端支持程度见https://taro-docs.jd.com/taro/docs/react#%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F

### 5.内置组件/Props
Taro使用React,所有内置组件都必须从`@tarojs/components`引入，组件的Props遵从大驼峰命名规范
```
// Taro写法
    import { View } from '@tarojs/components'
    <View hoverClass='test' />

// 小程序写法
<view hover-class='test' />
```
### 6.事件
在Taro中事件遵从小驼峰命名规范，所有内置事件名以`on`开头,在事件处理函数中第一个参数时事件本身，可以通过调用`stopPropagation`来组织冒泡。
```
function Comp () {
  // 只有 onClick 对应 bindtap
  // 其余内置事件名
  function clickHandler (e) {
    e.stopPropagation() // 阻止冒泡
  }

  function scrollHandler () {
    //
  }
  return <ScrollView onClick={clickHandler} onScroll={scrollHandler} />
}
```
## 完结 2020/10/29
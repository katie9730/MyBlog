## Web三大标准
- 结构：HTML
- 样式：CSS
- 行为：JS
    - ECMAScript
    - BOM (浏览器专有)
    - DOM (浏览器专有)

## 微信小程序(应用)
- 结构：WXML
    - 不是HTML
    - 遵循XML语法
    - 常用标签
        - <view>：类似div
        - <text>：类似<font><span>
        - <image>：类似<img>
            - 图片记得设置宽度
            - 图片记得按照需求设置缩放模式（model='aspectFill'）
        - <navigator>：类似<a>
    - 组件
        - 轮播图组件 <swipter> 默认150 
- 样式: WXSS
    - rpx单位 (基于750分辨率自动计算，设计稿也是750px)
    - 样式导入 import "*.wxss"
- 行为: JS
    - ECMAScript
    - wx对象（微信小程序封装顶级对象）
    - 注意：微信小程序里没有BOM和DOM的概念
- 配置: *.json
    - 非常严格的JSON格式
        - 必须双引号
        - 注释不可用
    - app.json
        - pages：配置项目的页面路径
        - window：配置项目窗口表现（标题、导航颜色等）
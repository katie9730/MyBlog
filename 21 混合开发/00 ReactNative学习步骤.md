### RN学习说明
1. ReactNative是基于React这门框架的语法来进行开发的。
2. RN中，提供了移动端专门的一些组件，所以一些网页中使用的元素，如div，p，img都不能用了，只能使用RN固有的组件。
3. 最终，开发出来的项目是要运行到手机上的，那么如何把一个RN的项目，完整的发布到手机上运行呢，这时候就需要结合安卓的签名打包步骤，并使用RN提供的打包命令，进行完整apk文件的发布，最终发布出来的就是Release版本的项目了，然后上传到应用商店里去。

### 手机的相关配置
1. 使用数据线，把手机连接到电脑上
2. 运行`adb devices`的命令，这个命令是安卓开发环境提供的
3. 需要先开启手机`开发者模式`
4. 如果开启开发者模式之后，还是看不到设备，则尝试安装`豌豆荚`这样的工具，让这些工具帮助你在电脑上安装手机的驱动
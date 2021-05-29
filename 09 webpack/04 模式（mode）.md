提供mode配置选项，告知webpack使用相应模式的内置优化。

#### 1.用法
```
//在配置中提供mode选项
module.export = {
    mode.'production'
}
//从CLI参数中传递
webpack --mode=production
```
用CLI参数传递支持以下字符串值
+ development:将 process.env.NODE_ENV 的值设为 development。启用 NamedChunksPlugin 和 NamedModulesPlugin。

+ production:将 process.env.NODE_ENV 的值设为 production。启用 FlagDependencyUsagePlugin, FlagIncludedChunksPlugin, ModuleConcatenationPlugin, NoEmitOnErrorsPlugin, OccurrenceOrderPlugin, SideEffectsFlagPlugin 和 UglifyJsPlugin.
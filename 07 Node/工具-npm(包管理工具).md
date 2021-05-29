#### npm解说
##### npx是什么
npm version >= 5.2.0开始，自动安装npx。
npx会帮忙执行依赖包里的二进制文件。

##### npx解决了什么
假若非全局安装了测试工具Mocha，并在项目中调用Mocha。
```
// 使用npx之前
./node_modules/.bin/mocha -v

// 使用npx之后
npx mocha -v
```
##### npx的原理
npx会自动查找当前依赖包中的可执行文件，如果找不到，就会去PATH里找，如果以然找不到，就会帮忙安装。
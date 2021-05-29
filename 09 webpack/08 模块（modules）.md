#### 1.概念
在模块化编程中，开发者将程序分解成离散功能块，并称之为模块。   

每个模块具有比完整程序更小的接触面，使得校验、调试、测试轻而易举。 精心编写的模块提供了可靠的抽象和封装界限，使得应用程序中每个模块都具有条理清楚的设计和明确的目的。

Node.js 从最一开始就支持模块化编程。然而，在 web，模块化的支持正缓慢到来。在 web 存在多种支持 JavaScript 模块化的工具，这些工具各有优势和限制。webpack 基于从这些系统获得的经验教训，并将模块的概念应用于项目中的任何文件。

#### 2.什么是webpack模块
对比Node.js模块，webpack模块能够以各种方式表达它们的依赖关系。如下：
+ ES2015 `import`语句
+ CommonJS `require()`语句
+ AMD `define` 和 `require`语句
+ css/sass/less文件中的`@import`语句
+ 样式`url(...)`或HTML文件`<img src=...>`中的图片链接

#### 3.支持的模块类型
webpack通过loader可以支持各种语言和预处理器编写模块。loader描述了webpack如何处理非JavaScript模块，并且在bundle中引入这些依赖。webpack社区已经为各种流行语言和语言处理器构建了loader，包括：
+ CoffeeScript
+ TypeScript
+ ESNext（Bable）
+ Sass
+ less
+ Stylus
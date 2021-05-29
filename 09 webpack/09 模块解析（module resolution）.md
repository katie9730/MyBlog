#### 1.概念
resolver是一个库，用于帮助找到模块的绝对路径。一个模块可以作为另一个模块的依赖模块，然后被后者引用，如下：
```
import foo from 'path/to/module'
//或者
require('path/to/module')
```
所依赖的模块可以是来自应用程序代码或第三方的库。resolver帮助webpack找到bundle中需要引入的模块代码，这些代码在包含在每个require/import语句中。当打包模块时，webpack使用enhanced-resolve来解析文件路径。

#### 2.webpack中的解析规则     
使用enhanced-resolve,webpack能够解析三种文件路径：
**2.1 绝对路径**
```
import '/home/me/file';
import 'c:\\Users\\me\\file';
```
**2.2 相对路径**
```
import '../src/file1';
import './file2';
```    
在这种情况下，使用 import 或 require 的资源文件(resource file)所在的目录被认为是上下文目录(context directory)。在 import/require 中给定的相对路径，会添加此上下文路径(context path)，以产生模块的绝对路径(absolute path)。

**2.3 模块路径**
```
import 'module';
import 'module/lib/file';
```
模块将在 resolve.modules 中指定的所有目录内搜索。 你可以替换初始模块路径，此替换路径通过使用 resolve.alias 配置选项来创建一个别名。

#### 3.解析
Loader 解析遵循与文件解析器指定的规则相同的规则。但是 resolveLoader 配置选项可以用来为 Loader 提供独立的解析规则。

#### 4.缓存
每个文件系统访问都被缓存，以便更快触发对同一文件的多个并行或串行请求。在观察模式下，只有修改过的文件会从缓存中摘出。如果关闭观察模式，在每次编译前清理缓存。
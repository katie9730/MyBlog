#### 1.概念
HTML 是网页使用的语言，定义了网页的结构和内容。浏览器访问网站，其实就是从服务器下载 HTML 代码，然后渲染出网页。

#### 2.网页基本概念
+ 标签
+ 元素：每个标签都是一个节点，称为网页元素。比如<p>标签对应网页的p元素。元素可分为两类。块元素和行内元素。
+ 属性：标签的额外信息，使用空格与标签名和其他属性分隔。推荐使用双引号。注意属性名对于大小写不敏感。

#### 3.网页的基本标签
+ <!doctype>:表示文档类型，告诉浏览器如何解析网页。然后浏览器就会按照HTML5的规则处理网页。
+ <html>:网页的顶层容器，称为根元素。该标签的lang属性，则表示网页内容默认的语言。
+ <head>:放置网页的元信息。为网页渲染做准备。
    - <meta>：设置网页的元数据。
    - <link>：连接外部样式表。
    - <title>：设置网页标题。
    - <style>：放置内嵌的样式表。
    - <script>：引入脚本。
    - <noscript>：浏览器不支持脚本时，所要显示的内容。
    - <base>：设置网页内部相对 URL 的计算基准。
+ <meta>:用于设置或说明网页的元数据。
    - name属性：表示元数据名字
    - content属性：表示元数据的值
    - charset属性：指定网页内容的编码方式。一般使用UTF-8。
+ <title>:网页的标题。
+ <body>:网页的主体内容。

#### 4.空格和换行
+ HTML语言有自己的空格处理规则。标签内容的头部和尾部的空格，一律忽略不计。
+ 会将文本里面的换行符（\n）,回车符（\r）,替换成空格。

#### 5.注释
+ <!---->

## 完结 2019/9/6
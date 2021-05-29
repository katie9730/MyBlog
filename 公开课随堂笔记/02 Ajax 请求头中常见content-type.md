HTTP协议是以ASCLL码传输，建立在TCP/IP协议之上的应用层中。规范把HTTP请求分为三个部分：
+ 状态行
+ 请求头（服务器通常根据请求头(headers)中的Content-Type字段来获知请求中的消息主题的编码方式，然后再对主体进行解析。）
+ 消息主体（提交的数据必须放在这里，但没有限制编码方式。）
******
##### 1.application/x-www-form-urlencoded(浏览器原生支持；最常见,且为默认)    
假若不设置enctype,那么默认会以这个方式提交数据。    
+ step1：请求头为Content-Type为application/x-www-form-urlencoded
+ step2：消息主体为key1=val1&key2=val2方式进行编码
> 注意：    
1). 若用js写ajax请求，则需要加上setRequestHeader("Content-type","application/x-www-form-urlencoded"),否则无法解析。     
2). form表单存在默认事件。可以用form表单上加onsubmit="return false",或者不用form标签来阻止事件。   
js使用e.preventDefault()或return false来阻止事件。      
IE/jq使用return false来阻止事件。

##### 2.multipart/form-data(浏览器原生支持；若需要表单上传文件时，则form中的enctype为此值)
+ step1：首先生成boundary用于分割不同的字段，避免与正文重复，boundary既长又复杂。
+ step2：Content-Type为mutipart/form-data
+ 消息主体组成：分为多部分，每部分以--boundary开头，紧接为内容描述信息，然后回车，最后为具体内容(文本or二进制)。若传输的是文件，则需包含文件名和文件类型。最后以--boundary标语结束。

##### 3.application/json(序列化后的JSON字符串)
+ JSON格式支持比键值对复杂得多的结构化数据
+ 有些服务端语言(eg:php)无法通过$_post对象从请求中获得内容。解决方式：在请求头中Content-Type为application/json时，从PHP:input里获得原始输入流，再json_decode成对象。

##### 4.text/html   
XML不能更好的适用于数据交换，是面向数据的;JSON是面向对象和结构的。    
如何选择使用
+ XML存储数据：存储配置文件等需要结构化存储的地方使用
+ JSON：数据传输、数据交互
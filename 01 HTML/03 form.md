```
HTML多媒体标签---<Embed>
<embed src="文件路径" width=value height=value hidden=hidden_value autostart=auto_value loop=loop_value ></embed>
hidden:是否隐藏
autostart：是否自动播放
loop：是否循环播放

表单标签---<form>
<form name="form_name" action="url" method="get/post"></form>
Name:表单名称
Method：浏览器传送到服务器的传送方式，默认为get；
Action：表单处理程序的位置

文本框
<input type="text" name="..."  size="..."  maxlength="..." value="...">
type="text",单行文本输入框。
name：文本框名称，独一无二的名称。
size：文本框宽度，单位是单个字符宽度。
maxlength：最多的输入字符数。
value：文本框初始值。

密码框
<input type="password" name="..." size="..." maxlength="...">

按钮
普通按钮
<input type="button" value="..." name="...">
提交按钮
<input type="submit" value="提交">
可将表单里的信息提交给表单里的action所指向的文件。
重置按钮

单选框和复选框
单选框
<input type="radio" name="..." value="..." cheched>
 2.复选框
<input type=checkbox name="..." value="..." checked>
checked:默认选中
value：选中后传送到服务器端的值
name：单选框的名称

文件输入框
<input type="file" name="...">

下拉框（select）
<select name="fruit">
<option value="apple">苹果</option>
<option value="orange">桔子</option>
<option value="mango">芒果</option>
</select>
若要复选，则<select name="fruit" multiple>

多行输入框（textarea）
<textarea name="yoursuggest" cols="50" rows="3"></textarea>

meta标签设定禁用缓存
<meta http-equiv="pragma" content="no-cache">
或者》<meta http-equiv="cache-control" content="no-cache">

什么是Css Hack？
一般来说是针对不同的浏览器写不同的Css，就是Css Hack。IE浏览器Hack一般分为三种，条件Hack、属性级Hack、选择符Hack。
```
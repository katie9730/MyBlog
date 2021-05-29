#### 1.表单描述
表单（<form>）用来收集用户提交的数据，发送到服务器。比如，用户提交用户名和密码，让服务器验证，就要通过表单。    
注意一：表单里面的<button>元素如果没有用type属性指定类型，那么默认就是submit控件。
注意二：除了submit提交表单，也可使用表单元素的submit()方法，通过脚本提交表单。
注意三：reset()方法可以重置所有控件的值。

#### 2.FormData对象
**2.1 概述**
表单数据以键值对的形式向服务器发送，有时候会通过脚本完成过程，构造和编辑键值对。然后通过`XMLHttpRequest.send()`方法发送。    
FormData首先是一个构造函数，用来生成实例。参数为表单元素，且可选。
```
var formdata = new FormData(form)
```

**2.2 FormData实例方法**
+ FormData.get(key)：参数为键名。获取指定键名对应的键值。若存在多个，则返回第一个键值对的键值。
+ FormData.getAll(key)：返回数组。
+ FormData.set(key, value):设置指定键名的键值。若键名不存在，则添加键值对或者更新。如果第二个参数为文件，可第三个参数是文件名。
+ Form.delete(key):删除一个键值对，参数为键名。
+ FormData.append(key, value):添加一个键值对。
+ FormData.has(key):返回布尔值，表示是否具有该键名的键值对。
+ FormData.keys():返回一个遍历器对象，用于for...of循环遍历键名。
+ FormData.values():返回一个遍历器对象，用于for...of循环遍历键值。
+ FormData.entries():返回一个遍历器对象，用于for...of循环遍历键值对。

#### 3.表单的内置验证
**3.1 自动校验**
表单提交时，浏览器允许开发者指定一些条件，则会自动验证是否符合条件。

**3.2 checkValidity()**
除了提交表单浏览器自动校验表单，还可手动触发表单的校验。通过checkValidity()方法，用于手动触发校验。方法返回布尔值，true为通过校验，false为没有通过校验。
```
// 触发整个表单的校验
form.checkValidity()
// 触发单个表单控件的校验
formControl.checkValidity()
```

**3.3 willValidate属性**
返回布尔值，表示控件是否在提交时进行校验。
```
var input = document.querySelector('#name');
input.willValidate  //true
```

**3.4 ValidationMessage属性**
返回字符串，表示控件不满足校验时，提示的文本。以下两种情况，返回空字符串
+ 该控件不会在提交时自动校验
+ 该控件满足校验条件

**3.5 setCustomValidity()**
用来定制校验失败时的报错信息。接受一个字符串作为参数，为定制的报错信息。若为空字符串，则上次设置的报错信息被清除。

**3.6 validity属性**
返回一个ValidityState对象，包含当前状态校验信息。它对象有多个属性，且不在此一一解释。

**3.7 表单的novalidate属性**
用于关闭浏览器的自动校验。

#### 4.enctype属性
表单可用四种编码，向服务器发送数据。编码格式由表单的enctype属性决定。

**4.1 Get方法**
若使用Get方法发送数据，enctype属性无效。
```
<form action="register.php" method="get" onsubmit="AJAXSubmit(this); return false"></form>

//数据将由以下格式发出
?foo=bar&baz=The%20first%20line.%0AThe%20second%20line.
```

**4.2 application/x-www-form-rulencoded 数据默认为此格式发送**
使用Post发送数据，且省略enctype属性。
```
<form
  action="register.php"
  method="post"
  onsubmit="AJAXSubmit(this); return false;"
>
</form>

//数据由以下格式发出
Content-Type: application/x-www-form-urlencoded

foo=bar&baz=The+first+line.%0D%0AThe+second+line.%0D%0A
```

**4.3 text/plain**
使用Post发送数据，enctype属性为text/plain，数据将以纯文本格式发送。
```
<form
  action="register.php"
  method="post"
  enctype="text/plain"
  onsubmit="AJAXSubmit(this); return false;"
>
</form>

//数据由以下格式发出
Content-Type: text/plain

foo=bar
baz=The first line.
The second line.
```

**4.4 multipart/form-data**
使用Post发送数据，enctype属性为multipart/form-data，则数据以混合格式发送。
```
<form
  action="register.php"
  method="post"
  enctype="multipart/form-data"
  onsubmit="AJAXSubmit(this); return false;"
>
</form>

//数据由以下格式发出
Content-Type: multipart/form-data; boundary=---------------------------314911788813839

-----------------------------314911788813839
Content-Disposition: form-data; name="foo"

bar
-----------------------------314911788813839
Content-Disposition: form-data; name="baz"

The first line.
The second line.

-----------------------------314911788813839--
```

#### 5.文件上传
用户上传文件，也是通过表单。通过输入框选择本地文件，提交表单，浏览器则会把这个文件发送到服务器。      
+ 请求方式：post
+ enctype属性：multipart-form-data。enctype属性决定HTTP头信息的Content-Type字段值，默认为application/x-www-form-urlencoded。不过上传文件时则需改成multipart/form-data。
```
<form method="post" enctype="multipart/form-data">
  <div>
    <label for="file">选择一个文件</label>
    <input type="file" id="file" name="myFile" multiple>
  </div>
  <div>
    <input type="submit" id="submit" name="submit_button" value="上传" />
  </div>
</form>

//新建一个FormData实例对象，模拟发送到时服务器的表单数据，把选中的文件添加到这个对象上面。
var formData = new FormData();
for (var i = 0; i < files.length; i++) {
  var file = files[i];

  // 只上传图片文件
  if (!file.type.match('image.*')) {
    continue;
  }

  formData.append('photos[]', file, file.name);
}

// 最后，使用Ajax向服务器上传头文件
var xhr = new XMLHttpRequest();xhr.open('POST', 'handler.php', true);
xhr.onload = function () {
  if (xhr.status !== 200) {
    console.log('An error occurred!');
  }
};
xhr.send(formData);
```
## 完结 2019/9/5
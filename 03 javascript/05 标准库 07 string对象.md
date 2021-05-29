#### 1. 概述
string对象是javaScript原生提供的三个包装对象之一，用来生成字符串对象。
```
var s1 = 'abc'
var s2 = new String('abc')

typeof s1 // 'string'
typeof s2 // 'object'

s2.valueOf() // 'abc'
```

#### 2.静态方法
静态方法是指定义在对象本身，而不是定义在对象实例的方法。
- String.fromCharCode()：该方法的参数是一个或多个数值，代表Unicode码点，返回值是这些码点组成的字符串。
```
String.fromCharCode() // ''
String.fromCharCode(97) // 'a'
String.fromCharCode(104,101,108,108,111) // 'hello'
```

#### 3.实例属性
- String.prototype.length：返回字符串的长度。

#### 4.实例方法
##### 4.1 String.prototype.charAt()
返回指定位置的字符，参数是从0开始编码的位置。
```
var s = new String('abc')
s.charAt(1) // 'b'
s.charAt(s.length -1) // 'c'
```
##### 4.2 String.prototype.charCodeAr()
返回字符串指定位置的Unicode码点。相当于`String.fromCharCode()`逆操作。

##### 4.3 String.prototype.concat()
用于链接两个字符串，返回一个新字符串，不改变原字符串。
```
var s1 = 'abc'
var s2 = 'def'
s1.concat(s2) // 'abcdef'
s1 // 'abc'
```
##### 4.4 String.prototype.slice()
从原字符串取出字符串并返回，不改变原字符串，第一个参数是子字符串的开始位置，第二个参数是子字符串的结束位置。
```
'JavaScript'.slice(0, 4) // 'java'
```

##### 4.5 String.prototype.subString()
用于从原字符串取出子字符串并返回，不改变原字符串，跟slice方法很相像。他的第一个参数表示子字符串的开始位置，第二个参数表示结束位置(返回结果不含该位置)。不建议使用subString方法，应该优先使用slice。

##### 4.6 String.prototype.subStr()
用于从原字符串取出子字符串并返回，不改变原字符串，跟slice和substring方法的作用相同。
substr方法的第一个参数是子字符串的开始位置（从0开始计算），第二个参数是子字符串的长度。
```
'JavaScript'.substr(4, 6) // 'Script'
```

##### 4.7 String.prototype.indexOf(), String.prototype.lastIndexOf()
indexOf方法用于确定一个字符串在另一个字符串中第一次出现的位置。返回结果是匹配开始的位置。返回-1则为不匹配。
```
'hello world'.indexOf('o') // 4
'JavaScript'.indexOf('script') // -1
```

##### 4.8 String.prototype.trim()
用于去除字符串两端的空格，返回一个新字符串，不改变原字符串。
```
' hello world '.trim()  // hello world
```

##### 4.9 String.prototype.toLowerCase(),String.prototype.toUpperCase()
`toLowerCase`方法用于将一个字符串全部转为小写，`toUpperCase`则是全部转为大写。他们都返回一个新字符串，不改变原字符串。

##### 4.10 String.prototype.match()
用于确定原字符串是否匹配某个字符串，返回一个数组，成员为匹配的第一个字符串。如果没有找到匹配，则返回null。
```
'cat, bat, sat, fat'.match('at') // ['at']
'cat, bat, sat, fat'.match('xt') // null
```

##### 4.11 String.prototype.search(), String.prototype.replace()
`search`方法基本等同于`match`,但是返回值为匹配的第一个位置。如果没有找到匹配，则返回`-1`。
```
'aaa'.replace('a', 'b') // 'baa'
```

##### 4.12 String.prototype.split()
按照给定规则分割字符串，返回一个由分割出来的子字符串组成数组。
`a|b|c`.split('|') // ['a', 'b', 'c']

##### 4.13 String.prototype.localeCompare()
localeCompare方法用于比较两个字符串，返回一个整数。小于0时，表示第一个字符串小于第二个字符串；等于0时，表示两者相等；大于0时，表示第一个字符串大于第二个字符串。

******
## 完结

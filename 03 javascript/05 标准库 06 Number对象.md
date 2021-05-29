#### 1.概述
`Number`对象是数值对应的包装对象，可以作为构造函数使用，也可以作为工具函数使用。
- 作为构造函数时，用于生成值为数值的对象
```
var n = new Number(1)
typeof n // 'object'
```

#### 2.静态属性
- Number.POSITIVE_INFINITY：正的无限，指向Infinity。
- Number.NEGATIVE_INFINITY: 负的五险，指向-Infinity。
- Number.NaN:表示非数值，指向NaN。
- Number.MIN_VALUE:表示最小的正数。
- Number.MAX_SAFE_INTEGER:表示能够精确的最大正整数。
- Number.MIN_SAFE_INTEGER:表示能够精确表示的最小整数。

#### 3.实例方法
- Number.prototype.toString():用来将一个数值转为字符串形式。`(10).toString() // 10`
- Number.prototype.toFixed():先将一个数转为指定位数的小数，然后返回这个小数对应的字符串
```
(10).toFixed(2) // '10.00'
10.005.toFixed(2) // '10.01'
```
- Number.prototype.toExponential():用于将一个数转为科学计数法形势。
```
(10).toExponential() // '1e+1'
```
- Number.prototype.toPrecision():用于将一个数转为指定位数的有效数字。
```
(12.34).toPrecision(3) // 12.34
```
- Number.prototype.toLocalString():接受一个地区吗作为参数，返回一个字符串，表示当前数字在该地区的当地书写方式。注意，该方法如果使用浏览器不认识的地区吗，就会抛出错误。
```
(123).toLocaleString('zh-Hans-CN-u-nu-hanidec')
// "一二三"
```

#### 4.自定义方法
Number.prototype对象上面可以自定义方法，被Number的实例继承。
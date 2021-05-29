## Flex 布局
- 传统布局
    - 盒子模型
        - display:block
        - display:inline
        - display:inline-block
    - 浮动流
    - 定位流
- 伸缩盒（弹性）布局
    - 传统属性（父元素）
         - display-flex
            - 让父子元素变成伸缩盒布局
            - 特征：子元素默认水平排列
        - flex-direction（flex方向）
        - justify-content（主轴对齐）
            - center
            - space-between
        - align-items（交叉轴）
            - center
            - flex-end
        - flex-wrap （伸缩盒换行）
    - 子元素（复合写法）
        - flex：0 1 auto
            - flex：伸 缩 固定值
        - flex实现栅格化
           - 注意：flex和width其实有冲突
                - flex级别更高
                - flex和width同时

## box-sizing
- content-box  是默认值。如果你设置一个元素的宽为100px，那么这个元素的内容区会有100px 宽，并且任何边框和内边距的宽度都会被增加到最后绘制出来的元素宽度中。
- border-box 告诉浏览器去理解你设置的边框和内边距的值是包含在width内的。也就是说，如果你将一个元素的width设为100px,那么这100px会包含其它的border和padding，内容区的实际宽度会是width减去border + padding的计算值。大多数情况下这使得我们更容易的去设定一个元素的宽高。

> 补充    
> iphone6中，375为逻辑分辨率，750px为物理分辨率

> 出处  
> [Flex布局教程语法：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html) 摘自阮一峰
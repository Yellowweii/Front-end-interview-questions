#### rem 和 em 的区别？移动端适配怎么做？（三种）

rem 是相对于根元素 html 的字体大小来计算的。em 是相对于当前元素的字体大小来计算的，它通常会继承父元素的字体大小。<br>
移动端适配：<br>
1、rem + flexible.js<br>
2、flex 布局，百分百布局<br>
3、媒体查询<br>
4、vw 和 vh

#### 使用 Float 进行布局容易产生什么问题？如何解决？

子元素在设置 float 后会脱离文档流，造成父元素高度塌陷<br>
解决方式：<br>
父元素设置高度<br>
清除浮动

#### 说一下 css 盒模型

CSS 盒模型由四部分组成：外边距(margin)，边框(border)，内边距(padding)，内容(content)<br>
box-sizing 属性：content-box(算元素的总宽度和高度时，不包含内边距和边框，只有内容区的大小)，border-box(内外边距不影响盒子宽度和高度)

#### 清除浮动有哪些方式？

1、额外标签法：在父盒子末尾添加一个块级标签，加上 clear:both 属性<br>
2、给父盒子添加伪元素<br>
3、给父盒子添加 overflow:hidden 属性

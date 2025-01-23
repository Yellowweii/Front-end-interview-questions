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

#### CSS 中隐藏元素的方法有哪些？

1、display: none;：将元素完全隐藏，不占据任何空间<br>
2、visibility: hidden;：将元素隐藏，但仍占据空间<br>
3、opacity: 0;：将元素透明化，但仍占据空间

#### CSS 选择器有哪些、优先级如何？

内联样式 > ID 选择器 > 类选择器、伪类、属性选择器 > 标签选择器、伪元素选择器 > 通用选择器

#### 单行元素的文本省略，多行元素的文本省略

//单行省略<br>
{<br>
white-space: nowrap; /_ 不换行 _/<br>
overflow: hidden; /_ 隐藏溢出的文本 _/<br>
text-overflow: ellipsis; /_ 显示省略号 _/<br>
}<br>
//多行省略<br>
{<br>
display: -webkit-box; /_ 使用弹性盒模型 _/<br>
-webkit-box-orient: vertical; /_ 垂直排列子元素 _/<br>
overflow: hidden; /_ 隐藏超出区域的文本 _/<br>
-webkit-line-clamp: 3; /_ 限制显示 3 行 _/<br>
text-overflow: ellipsis; /_ 溢出显示省略号 _/<br>
}

#### CSS 样式表根据所在网页的位置，可分为哪几种样式表？

1、内联样式表：适合单个元素快速调整样式<br>
2、内部样式表：适合单一页面样式管理<br>
3、外部样式表：适合网站整体样式统一管理，尤其适合大型项目

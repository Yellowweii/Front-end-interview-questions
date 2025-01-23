#### HTML5 新增的元素

1、新增了许多语义化标签：header、footer、article、section、nav、aside...<br>
2、新增了一些多媒体元素：video、audio<br>
3、新增了一些表单类型和属性：type="email", type="tel", type="search",type="file", placeholder, required, autocomplete

#### 说一说 title 和 alt 属性

title 属性用于为 HTML 元素提供额外的描述性信息，通常是当用户将鼠标悬停在该元素上时显示<br>
alt 主要用于为图片元素提供描述文本。当图像无法显示时，alt 内容会被显示在图片的位置，帮助用户了解图片的内容

#### html 语义化标签的好处？

1、增强 SEO：搜索引擎更容易理解页面的内容，从而提升排名<br>
2、提升代码的可读性和可维护性：便于开发者理解和维护代码

#### iframe 是什么？有什么缺点？

iframe 是 HTML 中的一个标签，用于在当前页面中嵌套另一个 HTML 页面。它的作用是将外部的网页作为一个子页面嵌入到父页面中，形成一个独立的、内嵌的浏览器视图。<br>
缺点：<br>
1、iframe 会在父页面中额外加载一个独立的页面，这增加了额外的 HTTP 请求，可能导致页面加载速度变慢<br>
2、搜索引擎通常不会索引 iframe 中的内容，所以 iframe 无法帮助父页面提升 SEO

#### HTML 全局属性有哪些?

HTML 全局属性是可以应用于所有 HTML 元素的属性。常见的全局属性包括：<br>
id：元素的唯一标识符。<br>
class：元素的类名，用于指定样式或脚本。<br>
style：内联 CSS 样式，定义元素的样式。<br>
title：为元素提供额外的信息，通常是鼠标悬停时显示的提示文本

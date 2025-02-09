- [1、HTML5 新增的元素？](#html5-新增的元素)
- [2、说一说 title 和 alt 属性](#说一说-title-和-alt-属性)
- [3、html 语义化标签的好处？](#html-语义化标签的好处)
- [4、iframe 是什么？有什么缺点？](#iframe-是什么有什么缺点)
- [5、HTML 全局属性有哪些?](#html-全局属性有哪些)
- [6、说说超链接 target 属性的取值和作用？](#说说超链接-target-属性的取值和作用)
- [7、meta viewport 是做什么的，怎么写?](#meta-viewport-是做什么的怎么写)
- [8、你用过哪些 meta 标签属性?](#你用过哪些-meta-标签属性)
- [9、Canvas 和 SVG 有什么区别？](#canvas-和-svg-有什么区别)
- [10、`<script>`标签会不会阻塞 HTML 的执行?怎么解决?](#script标签会不会阻塞-html-的执行怎么解决)
- [11、`<script>`标签属性 defer 和 async 的区别是什么？](#script标签属性-defer-和-async-的区别是什么)



#### HTML5 新增的元素

1、新增了许多语义化标签：header、footer、article、section、nav、aside...<br>
2、新增了一些多媒体元素：video、audio<br>
3、新增了一些表单类型和属性：type="email", type="tel", type="search",type="file", placeholder, required, autocomplete<br>
4、新增了 canvas 和 svg 标签，用于绘制图像

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

#### 说说超链接 target 属性的取值和作用？

\_self：打开链接时，内容会在同一个浏览器窗口或标签页中加载。<br>
\_blank：打开链接时，会在一个新的浏览器窗口或标签页中加载目标页面。

#### meta viewport 是做什么的，怎么写?

meta viewport 是一个 HTML 元素，用于控制网页在移动设备上的显示和缩放行为。它通过设置 viewport 元素的属性，告诉浏览器如何调整页面的尺寸和缩放，以适应不同屏幕大小和分辨率的设备<br>
`<meta name="viewport" content="width=device-width, initial-scale=1.0, user-scalable=no" />`

#### 你用过哪些 meta 标签属性?

1、设置网页字符编码<br>
`<meta charset="UTF-8">`<br>
2、控制视口<br>
`<meta name="viewport" content="width=device-width, initial-scale=1.0">`<br>
3、网站描述<br>
`<meta name="description" content="这是一个提供高质量内容的网站">`<br>
4、网站关键词<br>
`<meta name="keywords" content="HTML, CSS, JavaScript, 开发, 教程">`<br>
5、页面刷新或重定向<br>
`<meta http-equiv="refresh" content="5;url=https://example.com">`

#### Canvas 和 SVG 有什么区别？

Canvas 的绘图是使用 JavaScript 直接在渲染上下文（2D 或 3D）上动态绘制完成的，放大会失真，缩小可能模糊；<br>
SVG 使用 XML 描述图形，可以通过 DOM 操作和样式表（CSS）动态修改；SVG 是矢量图形，无论放大或缩小，图像都不会失真；可以为 SVG 图形添加事件（如点击、悬停）。

#### `<script>`标签会不会阻塞 HTML 的执行?怎么解决?

默认情况下，当浏览器解析到`<script>`标签时，会立即停止解析 HTML `并且执行脚本，这可能会导致页面加载和渲染的阻塞。这是因为浏览器需要等待脚本的下载、编译和执行完成后才能继续解析和渲染后续的内容。特别是当script`标签在 head 头文件内时，会延长页面的首屏渲染时间，导致用户看到空白页面的时间变长。<br>
解决方案：<br>
1、将`<script>`放在 `<body>`的底部：这样可以确保页面的内容能够先加载和渲染完成，然后再加载和执行脚本，减少阻塞对用户体验的影响。<br>
2、使用 defer 属性：在`<script>`标签中添加 defer 属性，将脚本的执行迟到整个页面解析完成后再执行。使用 defer 属性可以保证脚本在文档完全解析后执行，不会阻塞页面的渲染。<br>
3、使用 async 属性：在`<script>`标签中添加 async 属性，使脚本以异步方式加载和执行，不会阻塞页面的解析和渲染。但要注意，async 属性会导致脚本的执行顺序不确定，适用于独立的脚本文件，脚本之间不存在依赖关系。<br>
4、动态加载脚本：通过 JavaScript 代码动态地创建`<script>`标签，使得动态脚本的下载和执行是异步的，不会干扰 HTML 的解析和渲染。
5、对 window 顶级对象使用事件侦听，window.addEventListener('load', function() {})，等到浏览器所有内容加载完毕后再执行 js 代码

#### `<script>`标签属性 defer 和 async 的区别是什么？

1、defer 属性：当浏览器解析到带有 defer 属性的`<script>`标签时，会异步下载脚本文件，但会延迟脚本的执行，直到 DOM 树解析完成。如果有多个带有 defer 属性的脚本文件，它们会按照在页面上出现的顺序进行延迟执行。defer 属性适用于需要等待整个页面加载完成后再执行的脚本，可以确保脚本在文档完全解析后执行，从而不会阻塞页面的渲染。<br>
2、async 属性：当浏览器解析到带有 async 属性的`<script>`标签时，会异步下载脚本文件，并且不会阻塞页面的解析和渲染，即下载和执行脚本的过程与页面的加载是并行进行的。如果有多个带有 async 属性的脚本文件，它们的执行顺序是不确定的，哪个脚本文件先下载完就先执行。async 属性适用于独立的脚本文件，脚本之间不存在依赖关系，并且脚本的加载和执行顺序不重要。

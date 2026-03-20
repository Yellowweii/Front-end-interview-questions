#### NextJs的Image组件为什么可以压缩图片的体积？

Next.js 的 next/image 组件在服务端做裁图片压缩、剪、格式转换时，底层就是用sharp来处理的，sharp是一个Node.js内置的一个图片处理引擎。

#### NextJs中SSG和SSR两种渲染机制的区别？

构建时间：SSG构建阶段生成HTML，SSR是服务器请求阶段生成HTML；<br>
数据实时性：SSG构建时数据就固定下来，SSR的数据是动态更新的；<br>
首屏速度：SSG在代码构建时就生成了HTML，加载极快；SSR的首屏速度取决于服务器的响应速度；<br>
页面数量：SSG适用于加载少量页面，数据量大会导致构建很慢；SSR适用于有大量页面需要加载的情况，不受页面总数的影响，按需加载。<br>

#### 谈一谈NextJs的Link组件。

1.它支持国际化路由显示<br>
2.它可以使当前视口内所有可见链接提前预加载，预加载内容是 对应页面的 JS bundle，JS Bundle 是指将页面相关的 JavaScript 代码打包成一个文件或一组文件。<br>

#### NextJs中App Router和Pages Router的区别？

1、路由：App Router中一个文件夹就是一个路由，而Pages Router中一个文件就是一个路由<br>
2、数据获取方式：App Router默认就是RSC，直接通过await fetch就可以实现SSR，而Pages Router则是通过getServerSideProps和getStaticProps来获取数据<br>
3、数据获取粒度：App Router因为RSC的关系，在组件层级就可以直接await fetch，而Pages Router的getServerSideProps / getStaticProps只能在页面级别使用<br>
4、页面Layout：App Router支持嵌套layout，每一层路由都可以有自己的页面布局，而Pages Router通过_app.tsx包裹所有页面，全局layout只有一层，灵活性差<br>
5、Js bundle更小：App Router RSC中的代码并不会被打包发送给浏览器，可以提高首屏的FCP，LCP性能，且RSC本身不参与 hydration，减少了 hydration error 的发生范围，而Pages Router会把所有页面代码打包发送给浏览器，bundle更大，且所有组件都需要 hydration，出现 hydration error的风险更高<br>

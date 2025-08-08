#### NextJs的Image组件为什么可以压缩图片的体积？

Next.js 的 next/image 组件在服务端做裁图片压缩、剪、格式转换时，底层就是用sharp来处理的，sharp是一个Node.js内置的一个图片处理引擎。
# 版本1.2

一、优化github pages：上传nuxt项目的源码到github后利用github action在github上完成构建和部署后接受访问（而非之前的“直接上传我本地构建后的代码”）

二、适配手机屏幕：完成tailwindCSS的屏幕适配，并且解决其与gsan之间的冲突bug（当gsan动画完成一半时我改变窗口大小，就会出现bug，这里就是解决这个bug）。

三、完成“markdown格式的开发者日志”页面：我下意识先问了ChatGPT如何继承markdown的渲染功能，但很快意识到我可以直接Google一下“nuxt markdown”，果然马上找到了nuxt官方所提供的nuxt content，它提供了包括markdown渲染等很多功能；实现开发者日志页面的过程中，我想到了要使用侧边栏，于是向ChatGPT询问说nuxt官方是否推荐了组件库，于是我了解到nuxt官方直接提供的“nuxt ui”，我用它来完成开发。
四、优化顶部导航栏：使用了nuxt官方提供的nuxt ui。
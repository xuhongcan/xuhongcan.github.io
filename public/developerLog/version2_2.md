
# 版本2.2

> 时间：26年6月8日

### 一、解决了一个简单bug：

~~~ powershell
 WARN  [Vue warn]: Failed to resolve component: Placeholder                                                                                                                                        02:52:14
If this is a native custom element, make sure to exclude it from component resolution via compilerOptions.isCustomElement. at <DeveloperLog>
at <RouteProvider>
at <RouterView>
at <NuxtPage>
at <Default>
at <AsyncComponentWrapper>
at <LayoutLoader>
at <NuxtLayoutProvider>
at <NuxtLayout>
at <App>
at <NuxtRoot>
 WARN  [Vue warn]: Component <Anonymous> is missing template or render function. at <Anonymous>                                                                                                    02:52:14
at <DeveloperLog>
at <RouteProvider>
at <RouterView>
at <NuxtPage>
at <Default>
at <AsyncComponentWrapper>
at <LayoutLoader>
at <NuxtLayoutProvider>
at <NuxtLayout>
at <App>
at <NuxtRoot>
~~~

- 很快找到了最重要的两个词：
  - `Failed to resolve component: Placeholder`：这是个标题，能看懂；而另一个标题有我不懂的`<Anonymous>`。
  - `at <DeveloperLog>`：因为只有这个组件是我写的，其他都是nuxt自己执行的。
- 所以打开`<DeveloperLog>`中找到`Placeholder`组件删掉就可以了，两个`WARN`都得到了解决。

### 二、解决了一个非常严重、而且很难解决的bug：

~~~ powershell
WARN Could not fetch from https://fonts.google.com/metadata/icons?key=material_symbols&incomplete=true. Will retry in 1000ms. 3 retries left. 02:22:13

WARN Could not fetch from https://fonts.google.com/metadata/icons?key=material_symbols&incomplete=true. Will retry in 1000ms. 2 retries left. 02:22:24


at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
at async $fetch2 (/D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/ofetch/dist/shared/ofetch.CWycOUEr.mjs:332:15)
at async /D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:572:16
at async Object.getItem (/D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:813:17)
at async /D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:571:22
at async /D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:863:32
at async Promise.all (index 1)
at async createUnifont (/D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:860:2)
at async createResolver (/D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/fontless/dist/index.mjs:295:18)

[cause]: fetch failed

  at node:internal/deps/undici/undici:13502:13
  at process.processTicksAndRejections (node:internal/process/task_queues:105:5)
  at async $fetchRaw2 (/D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/ofetch/dist/shared/ofetch.CWycOUEr.mjs:274:26)
  at async $fetch2 (/D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/ofetch/dist/shared/ofetch.CWycOUEr.mjs:332:15)
  at async /D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:572:16
  at async Object.getItem (/D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:813:17)
  at async /D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:571:22
  at async /D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:863:32
  at async Promise.all (index 1)
  at async createUnifont (/D:/ProjectCode/projects_202603/3.1.my-standalone-site/node_modules/unifont/dist/index.mjs:860:2)

[cause]: Connect Timeout Error (attempted address: fonts.google.com:443, timeout: 10000ms)

    at onConnectTimeout (node:internal/deps/undici/undici:2602:28)
    at Immediate._onImmediate (node:internal/deps/undici/undici:2568:35)
    at process.processImmediate (node:internal/timers:491:21)
    at process.callbackTrampoline (node:internal/async_hooks:130:17)
~~~


这个严重bug，让每次nuxt启动都要延迟30秒。

#### 解决过程

- 基本被Gemini和ChatGPT牵着走，全程无脑地尝试了很久。
- 最后靠ChatGPT完成debug（而Gemini发挥了0作用）
- 【自主debug能力有待提高】

#### 最终解决

> 原因：`"@nuxt/ui": "^4.8.2",`这个版本存在着这个bug，其解决方法是：Nuxt UI官方提供的关闭字体自动优化的方法（下面添加的三行）。

~~~ ts
export default defineNuxtConfig({
  compatibilityDate: '2025-07-15',
  devtools: { enabled: false },
  modules: ['@nuxt/ui'],
  css: ['~/assets/css/main.css'],

  // 解决办法：添加了下面三行
  ui: {
    fonts: false
  }
})
~~~

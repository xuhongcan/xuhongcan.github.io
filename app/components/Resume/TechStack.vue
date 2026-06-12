<template>
  <div class="flex justify-center">
    <div v-html="html" class="prose dark:prose-invert w-[80vw] md:min-w-[60vw]"></div>
  </div>

</template>

<script lang="ts" setup>
const text = `
### 技术栈

    Vue3/Nuxt
    微信小程序
    uniapp
    Electron
    
    TailwindCSS
    SCSS
    TypeScript
    
    Git
    Vite

    Echarts
    markdown-it
    GSAP

    ChatGPT
    Vibe Coding
    根据需求画原型图

    ...
`
import MarkdownIt from 'markdown-it'
const md = new MarkdownIt();
const html = computed(() => md.render(text))

</script>

<style></style>
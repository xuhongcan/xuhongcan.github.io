<template>
  <div class="m-[10px]">
     <UTimeline :orientation="orientation" :default-value="5" :items="items" class="w-full" />
  </div>
</template>

<script lang="ts" setup>

// 屏幕响应式改变垂直or水平
import { useWindowSize } from '@vueuse/core'
const { width } = useWindowSize()
const orientation = computed(()=>{
  return width.value >=768?'horizontal':'vertical'
})



import type { TimelineItem } from '@nuxt/ui'

// 获取当前完整时间
const now = new Date()
// 格式化（常用格式：YYYY-MM-DD HH:mm:ss）
const formatTime = (date) => {
  const year = date.getFullYear()
  const month = String(date.getMonth() + 1).padStart(2, '0')
  const day = String(date.getDate()).padStart(2, '0')
  const hours = String(date.getHours()).padStart(2, '0')
  const minutes = String(date.getMinutes()).padStart(2, '0')
  return `${year}年${month}月${day}日 ${hours}:${minutes}`
}
// 使用
const nowStr = formatTime(new Date())

const items = ref<TimelineItem[]>([
  {
    date: '2023年6月10日（高考后第二天）',
    title: 'C语言',
    description: '开始接触编程',
    icon: 'i-lucide-rocket'
  },
  {
    date: '2023年7月25日',
    title: '后端基础',
    description: 'JavaSE、JavaWeb',
    icon: 'i-lucide-palette'
  },
  {
    date: '2023年9月11日',
    title: '【前端基础】',
    description: '开学，HTML、CSS、JS',
    icon: 'i-lucide-palette'
  },
  {
    date: '2023年9月~2024年8月',
    title: 'Java后端',
    description: 'SSM、SpringBoot、SpringCloud',
    icon: 'i-lucide-code'
  },
  {
    date: `2024年8月~2026年3月`,
    title: '【Vue3前端】',
    description: 'Vue3/Nuxt、微信小程序、uniapp、Electron',
    icon: 'i-lucide-check-circle'
  },
  {
    date: `2026年~至今（${nowStr}）`,
    title: '【继续学习】',
    description: 'Vibe Coding、墨刀画产品功能图',
    icon: 'i-lucide-check-circle'
  }
])

</script>

<style>

</style>
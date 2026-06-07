<template>
  <div class="flex flex-1">
    <USidebar
      v-model:open="open"
      collapsible="icon"
      rail
      :ui="{
        container: 'h-full',
        inner: 'bg-elevated/25 divide-transparent',
        body: 'py-0',
      }"
    >
    <div class="mt-25">
      <div v-for="(item, index) in developerLogList" :key="index">
        <UButton @click="activeIndex = index" size="xl" color="neutral" class="w-full">{{ item.name }}</UButton>
      </div>
    </div>

    </USidebar>

    <div class="flex-1 flex flex-col">
      <div class="flex-1 p-4">
        <UButton
          icon="i-lucide-panel-left"
          color="neutral"
          variant="ghost"
          aria-label="Toggle sidebar"
          @click="open = !open"
        />
        <Placeholder class="size-full" />

        <DeveloperLogMarkdown :markdownContent="markdownContent" />

      </div>
    </div>
  </div>
</template>


<script setup lang="ts">
const open = ref(true);

import type { TabsItem } from '@nuxt/ui'
const developerLogList = ref<TabsItem[]>([
  {
    id: 1,
    name: "1.1版本",
    filePath: "/developerLog/version1_1.md",
  },
  {
    id: 2,
    name: "1.2版本",
    filePath: "/developerLog/version1_2.md",
  },
])
const activeIndex = ref(0)

const markdownContent = ref('加载中...')

watch(activeIndex, async() => {
  markdownContent.value = await $fetch(developerLogList.value[activeIndex.value]?.filePath||"/developerLog/version1_1.md")
})

onMounted(async()=>{
  markdownContent.value = await $fetch(developerLogList.value[0]?.filePath||"/developerLog/version1_1.md")
})

</script>


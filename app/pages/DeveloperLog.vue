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
      <div class="flex items-center justify-between h-full">
        <div v-show="open" class="whitespace-nowrap">开发者日志：目录</div>
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
        <div>开发者日志：内容</div>
      </div>
    </div>
  </div>
</template>



<script setup lang="ts">
const open = ref(true);

//测试markdown-it
</script>


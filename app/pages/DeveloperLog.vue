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

        <article class="prose dark:prose-invert">
          <div v-html="html"></div>
        </article>
      </div>
    </div>
  </div>
</template>



<script setup lang="ts">
const open = ref(true);

import MarkdownIt from "markdown-it";
const md = new MarkdownIt();
const markdownContent = ref(`# 这是一个标题
这是一些文本内容。
- 列表项1
- 列表项2
`);
const html = computed(() => md.render(markdownContent.value));
</script>


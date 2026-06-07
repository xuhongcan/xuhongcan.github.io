<template>
  <article class="prose dark:prose-invert">
    <div v-html="html"></div>
  </article>
</template>

<script setup lang="ts">
const { markdownContent } = defineProps(['markdownContent'])

import MarkdownIt from "markdown-it";
const md = new MarkdownIt();

const html = computed(() => md.render(markdownContent));
</script>

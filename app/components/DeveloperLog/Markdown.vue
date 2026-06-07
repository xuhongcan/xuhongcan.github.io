<template>
  <article class="prose dark:prose-invert">
    <div v-html="html"></div>
  </article>
</template>

<script setup lang="ts">
interface Props {
  markdownContent: string;
}
const {markdownContent} = defineProps<Props>();

import MarkdownIt from "markdown-it";
const md = new MarkdownIt();

const html = computed(() => md.render(markdownContent));
</script>

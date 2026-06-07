<template>
  <UHeader :toggle="false">
    <template #title>
      <NuxtLink
        to="/"
        class="w-10 h-10 flex items-center justify-center rounded-lg transition"
      >
        ☰
      </NuxtLink>
    </template>
    
    <div class="select-none">许宏灿</div>

    <template #right>
      <UNavigationMenu :items="items" />
    </template>
  </UHeader>
</template>



<script setup lang="ts">
import type { NavigationMenuItem } from "@nuxt/ui";

const route = useRoute();

const items = computed<NavigationMenuItem[]>(() => [
  {
    label: "简历",
    to: "/resume",
  },
  {
    label: "视频",
    to: "/video",
  },{
    label: "日志",
    to: "/developerLog",
  },
]);
</script>
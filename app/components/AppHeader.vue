<template>
  <UHeader>
    <template #title>
      <NuxtLink
        to="/"
        class="w-10 h-10 flex items-center justify-center rounded-lg transition text-white"
      >
        ☰
      </NuxtLink>
    </template>
    
    许宏灿

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
    label: "拍摄",
    to: "/shoot",
  },
  {
    label: "演员",
    to: "/actor",
  },{
    label: "剪辑",
    to: "/filmEdit",
  },{
    label: "开发者日志",
    to: "/developerLog",
  },
]);
</script>
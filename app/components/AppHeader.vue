<template>
  <div
    class="h-14 px-4 bg-zinc-900 border-b border-zinc-800 flex items-center justify-between max-w-[100vw] overflow-hidden"
  >
    <!-- 左侧 -->
    <div class="flex items-center gap-2">
      <NuxtLink
        to="/"
        class="w-10 h-10 flex items-center justify-center rounded-lg hover:bg-zinc-800 transition text-white"
      >
        ☰
      </NuxtLink>
    </div>

    <!-- 右侧 -->
    <div class="flex items-center gap-3">
      <NuxtLink
        to="/shoot"
        class="w-28 h-10 flex items-center justify-center rounded-lg hover:bg-zinc-800 transition text-white"
      >
        拍摄
      </NuxtLink>

      <NuxtLink
        to="/actor"
        class="w-28 h-10 flex items-center justify-center rounded-lg hover:bg-zinc-800 transition text-white"
      >
        演员
      </NuxtLink>

      <NuxtLink
        to="/filmEdit"
        class="w-28 h-10 flex items-center justify-center rounded-lg hover:bg-zinc-800 transition text-white"
      >
        剪辑
      </NuxtLink>
    </div>
  </div>
</template>

<script setup>
</script>

<template>
  
  <header>
    <AppHeader></AppHeader>
  </header>

  <!-- <div>
    <slot></slot>
  </div> -->

  <div class="relative min-h-screen w-full">
    <div class="absolute inset-0 bg-[url(/img/img-bg3.png)] bg-cover bg-fixed opacity-30"></div>
    <div class="relative z-10">
      <slot></slot>
    </div>
    <div class="relative h-[10vh] md:h-[20vh]"></div>
  </div>

  

</template>

<script setup lang="ts">

</script>

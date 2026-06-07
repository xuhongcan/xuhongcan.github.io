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
      <div class="mt-25 flex flex-col">
        <div v-for="(item, index) in developerLogList" :key="index">
          <UButton
            @click="activeIndex = index"
            size="xl"
            color="neutral"
            class="w-full"
            >{{ item.name }}</UButton
          >
        </div>
        <UButton
          class="self-end my-7 bg-gray-500"
          color="neutral"
          variant="ghost"
          aria-label="Toggle sidebar"
          @click="open = !open"
        >折叠</UButton>
      </div>
    </USidebar>

    <div class="flex-1 flex flex-col">
      <div class="flex-1 p-4">
        <div class="w-full flex">
          <DeveloperLogMarkdown
            :markdownContent="markdownContent"
            class="lg:ml-[10vw]"
          />
        </div>
        <UButton
          color="neutral"
          variant="ghost"
          aria-label="Toggle sidebar"
          class="bg-gray-500"
          @click="open = !open"
        >折叠</UButton>
      </div>
    </div>
  </div>
</template>


<script setup lang="ts">
const open = ref(true);

interface DeveloperLogList {
  id: number;
  name: string;
  filePath: string;
}
const developerLogList = ref<DeveloperLogList[]>([
  {
    id: 1,
    name: "1.1版本",
    filePath: "/developerLog/version1_1.md",
  },
  {
    id: 2,
    name: "2.1和2.2版本",
    filePath: "/developerLog/version2_1.md",
  }
]);
const activeIndex = ref(0);

const markdownContent = ref("加载中...");

watch(activeIndex, async () => {
  markdownContent.value = await $fetch<string>(
    developerLogList.value[activeIndex.value]?.filePath ||
      "/developerLog/version1_1.md"
  );
});

onMounted(async () => {
  markdownContent.value = await $fetch<string>(
    developerLogList.value[0]?.filePath || "/developerLog/version1_1.md"
  );
});
</script>


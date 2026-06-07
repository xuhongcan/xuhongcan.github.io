<template>
  <!-- 第一屏：“向下滚动” -->
  <div class="select-none text-4xl text-white font-bold">向下滚动</div>
  <div class="h-[8vh] w-full"></div>
  <!-- 响应式屏幕适配：默认为移动端 -->
  <div class="flex flex-col items-center lg:flex-row lg:justify-around">
    <div
      id="trigger-1-img"
      class="w-[60vw] lg:w-[28vw] rounded-3xl overflow-hidden lg:m-20"
    >
      <img src="/img/img-xuhongcan.jpg" alt="个人图片" />
    </div>
    <div
      class="text-white font-bold flex flex-col items-center w-[80vw] lg:w-[28vw] lg:m-[80px]"
    >
      <div class="text-2xl w-full flex justify-around">
        <div>许宏灿</div>
        <div>18岁</div>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

let ctx: gsap.Context | null = null;

onMounted(() => {
  ctx = gsap.context(() => {
    gsap.registerPlugin(ScrollTrigger);
    gsap.defaults({ ease: "none", duration: 2 });

    const tl = gsap.timeline();
    tl.from("#trigger-1-img", {  opacity: 0, scale:0.5 }).to("#trigger-1-img", {  opacity: 1, scale:1.5 }).to("#trigger-1-img", {  opacity: 1, scale:1 })


    ScrollTrigger.create({
      animation: tl,
      trigger: "#trigger-1-img",
      start: "center center",
      end: "+=1400",
      scrub: true,
      pin: true,
    });
  });
});

onUnmounted(() => {
  ctx?.revert();
});
</script>

<template>
  
  <!-- 第二瓶：个人图片、文字、基本介绍、按钮 -->
      <div
        id="trigger-1"
        class="flex justify-around h-[80vh] w-[80vw] relative"
      >
        <div
          id="trigger-1-img"
          class="w-[28vw] rounded-3xl overflow-hidden absolute bottom-0 opacity-0"
        >
          <img src="/img/img-xuhongcan.jpg" alt="个人图片" />
        </div>
        <div
          id="trigger-1-text"
          class="text-white font-bold flex flex-col w-[28vw] items-center absolute"
        >
          <div class="text-2xl w-full flex justify-around">
            <div>许宏灿</div>
            <div>18岁</div>
          </div>
        </div>
      </div>
</template>

<script lang="ts" setup>

// 鼠标滚动动画
import gsap from "gsap";
import { ScrollTrigger } from "gsap/ScrollTrigger";

let ctx: gsap.Context | null = null;

onMounted(() => {
  ctx = gsap.context(() => {
    gsap.registerPlugin(ScrollTrigger);
    gsap.defaults({ ease: "none", duration: 2 });

    const tl = gsap.timeline();
    tl.to("#trigger-1-img", { width: "40vw", opacity: 1 }).to(
      "#trigger-1-img",
      { width: "28vw", opacity: 1, y: "-8vw", x: "-12vw", delay: 1.8 }
    );
    tl.from("#trigger-1-text", { x: "-12vw", opacity: 0 }).to(
      "#trigger-1-text",
      { x: "24vw", opacity: 1 }
    );
    ScrollTrigger.create({
      animation: tl,
      trigger: "#trigger-1",
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

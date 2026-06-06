<template>
  <header>
    <AppHeader></AppHeader>
  </header>

  <main>
    <!-- 遇到的问题： -->
    <!-- 1、先尝试了chatgpt推荐的vueUse的useElementVisibility后发现无法实现，又继续询问chatgpt后尝试了GASP的ScrollTrigger -->
    <!-- 2、使用了GSAP及其CscrollTrigger来制作鼠标滚动动画，学习并且写了尝试的代码后，
     出现报错“`Cannot read properties of undefined (reading 'querySelectorAll')`”，
     可迅速理解为：GSAP与Nuxt并不适配，于是找了Grok发起询问，得知我应该使用`v-gsap-nuxt`这个专门为Nuxt适配的GSAP模块。
     ————————结论：
     那么，当我以后使用新的框架时，应该先查找是否有专门适配该框架的库，而不是直接使用原生库，避免出现不兼容的问题。
     不过呢，其实先通过原生库来学习和理解动画的原理也是不错的，毕竟适配库可能会对原生库进行封装，隐藏掉一些细节，所以先学习原生库可以更好地理解动画的实现机制，然后再使用适配库来简化开发过程。
     -->
    <!-- 3、当我使用了v-gsap-nuxt以后，依然报了同样的错误，经过大概十几分钟的AI询问（问不出结果）和自己对官方文档的阅读理解，
        最后把某些代码写在了onBeforeMount生命周期函数中，才成功解决了问题。
        于是，我又尝试把v-gsap-nuxt库删除，改回原生库，发现依然成功运行。
        ————结论：不论原生库还是v-gsap-nuxt库，都能在Nuxt中成功使用ScrollTrigger。而v-gsap-nuxt的作用是让代码更简洁，把简单逻辑写在Nuxt的html中
     -->
    <!-- 4、以上从开始到完成第一个实例，大概花了3小时————只记得我45分钟的番茄钟，用了大概4个 -->

    <div
      class="bg-[url(/img/img-bg.jpg)] bg-cover bg-fixed min-h-[100vh] max-w-[100vw] flex flex-col items-center"
    >

      <div class="h-[42vh] w-full"></div>

      <!-- 第二屏：个人图片、文字、基本介绍、按钮 -->
      <HomeBasicInfomation></HomeBasicInfomation>
      <div class="h-[300vh] w-full"></div>

      <!-- <div>
        内容： 1、背景图片空屏，显示文字“向下滚动鼠标”
        2、个人图片、文字、基本介绍、按钮，随着鼠标依次上滑
        3、调色：显示一张未调色图片，然后滚动鼠标时，从右往左刮成已调色图片
        4、一行文字：基本介绍 5、多张图片列表
      </div> -->
    </div>
  </main>
</template>

<script setup lang="ts">
definePageMeta({
  layout: false,
});



</script>

<template>
  <div
    class="p-5 h-screen w-screen dark:bg-gray-950 flex flex-col items-center justify-center"
  >
    <div class="flex h-40 justify-center items-center">
      <div class="w-10 h-10 rounded-md bg-blue-500" ref="demo"></div>
      <div class="w-10 h-10 rounded-md bg-blue-800" ref="demo2"></div>
    </div>
    <div class="flex flex-col items-center gap-2 w-80">
      <h2 class="text-2xl text-gray-500">{{ text.num }} %</h2>
      <div class="h-1 rounded-full bg-blue-600" ref="bline"></div>
      <p class="text-gray-700 text-sm">- 进度是走不完的 -</p>
      <button
        class="shadow-md border py-1 px-4 rounded-md hover:bg-gray-100 dark:text-white dark:hover:bg-gray-800"
        @click="$router.push('/anima')"
      >
        直接进入
      </button>
    </div>
  </div>
</template>
<script setup lang="ts">
import gsap from "gsap";
const demo = ref();
const demo2 = ref();
const bline = ref();
const text = reactive({
  text: "Give me money",
  num: 0,
});
onMounted(() => {
  gsap.fromTo(
    [demo.value, demo2.value],
    {
      x: 200,
      opacity: 0,
    },
    {
      x: 0,
      rotation: -45,
      scale: 2,
      duration: 1,
      opacity: 1,
      onComplete() {
        lod();
      },
    }
  );
  gsap.to(text, {
    num: 99.99,
    duration: 2,
    delay: 1.1,
    repeat: -1,
  });
  gsap.to(bline.value, {
    width: "100%",
    duration: 2,
    repeat: -1,
  });
});

function lod() {
  gsap.fromTo(
    [demo.value, demo2.value],
    {
      x: -10,
      opacity: 0,
    },
    {
      x: 0,
      rotation: -45,
      duration: 1,
      opacity: 1,
      repeat: -1,
      yoyo: true,
      stagger: 0.1,
    }
  );
}
</script>

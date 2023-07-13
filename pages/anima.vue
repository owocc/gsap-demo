<template>
  <div
    class="h-screen pt-10 dark:bg-gray-900 text-blue-900 dark:text-blue-200 w-screen flex flex-col items-center gap-4"
  >
    <h1 class="text-2xl font-bold">- Time Line -</h1>
    <!-- 播放屏幕 -->
    <div
      class="w-[800px] dark:bg-gray-800 rounded-lg p-2 bg-gray-200 flex flex-col gap-2"
    >
      <div class="h-10 w-10 bg-blue-300 rounded-md" ref="a1"></div>
      <div class="h-10 w-10 bg-blue-400 rounded-md" ref="a2"></div>
      <div class="h-10 w-10 bg-blue-500 rounded-md" ref="a3"></div>
    </div>

    <div class="w-[800px] flex flex-col gap-1">
      <div class="text-center flex items-center justify-between">
        <div>
          <h3 class="text-3xl">{{ lineOptions.time.toFixed(2) }}</h3>
        </div>
        <div>
          <button
            class="border py-1 hover:bg-gray-100 dark:hover:bg-gray-800 px-4 rounded-md"
            @click="playOrPause"
          >
            {{ lineOptions.play ? "Pause" : "Play" }}
          </button>
        </div>
      </div>
      <div class="w-full flex h-3 justify-between">
        <div
          class="w-[1px] border-l"
          v-for="item in lineOptions.timer + 1"
          :key="item"
        ></div>
      </div>
      <div class="w-full h-6 p-1 bg-gray-200 rounded-sm dark:bg-gray-700">
        <div class="w-0 rounded-full bg-orange-400 h-full" ref="t1"></div>
      </div>
    </div>
    <button
      @click="navigateTo('/filp')"
      class="border py-2 p-4 w-24 hover:bg-gray-100 dark:hover:bg-gray-800 rounded-md"
    >
      Flip
    </button>
  </div>
</template>
<script setup lang="ts">
import gsap from "gsap";
import { Draggable } from "gsap/Draggable";

gsap.registerPlugin(Draggable);
const lineOptions = reactive({
  timer: 3,
  time: 0,
  play: true,
});
// 创建一条时间线
const tl = gsap.timeline({
  repeat: -1,
  yoyo: true,
  defaults: {
    duration: 1,
  },
});

const a1 = ref();
const a2 = ref();
const a3 = ref();
const t1 = ref();

// 自动播放一次动画
onMounted(() => {
  Draggable.create(a1.value, { bounds: "body", inertia: true });
  Draggable.create(a2.value, { bounds: "body", inertia: true });
  Draggable.create(a3.value, {
    bounds: "body",
    type: "rotation",
    inertia: true,
  });
  playAnima();
});
// 播放动画
const playAnima = () => {
  tl.to(lineOptions, {
    time: lineOptions.timer,
    duration: lineOptions.timer,
  });
  tl.to(
    t1.value,
    {
      width: "100%",
      duration: lineOptions.timer,
    },
    "<"
  );
  tl.to(
    a1.value,
    {
      x: 600,
      rotation: 75,
      scale: 1.5,
    },
    1
  );

  tl.to(
    a2.value,
    {
      x: 700,
      rotation: -65,
      scale: 2,
    },
    ">"
  );

  tl.to(
    a3.value,
    {
      x: 400,
      rotation: -35,
      scale: 3,
    },
    "<"
  );
};

const playOrPause = () => {
  if (lineOptions.play) {
    tl.pause();
  } else {
    tl.play();
  }
  lineOptions.play = !lineOptions.play;
};
</script>

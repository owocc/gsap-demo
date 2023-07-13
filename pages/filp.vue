<template>
  <div
    class="flex dark:bg-blue-950 dark:text-white w-screen h-screen flex-col justify-center items-center gap-10"
  >
    <h1 class="text-6xl text-red-400 font-black">Super Mario</h1>
    <div class="flex justify-center gap-2 items-center" ref="demos">
      <div class="h-10 w-10 bg-red-500 rounded-sm" v-for="item in 10"></div>
    </div>

    <div
      class="hover:scale-125 dark:border-orange-700 dark:hover:border-orange-300 dark:bg-red-500 hover:border-red-200 transition-all ease-in-out group w-80 border bg-gray-100 flex justify-center items-center h-40 rounded-lg overflow-hidden"
    >
      <Teleport to="#port" :disabled="!diaLogInfo.show">
        <img
          :src="img"
          alt=""
          ref="box"
          class="hover:scale-150 group-hover:scale-150 transition-all duration-200 ease-out group-hover:translate-y-4"
        />
      </Teleport>
    </div>

    <button
      class="py-2 px-4 min-w-[100px] dark:hover:bg-gray-700 dark:hover:text-orange-400 hover:bg-gray-100 hover:text-orange-500 transition-all duration-150 border rounded-full"
      @click="openDialog"
    >
      Open Dialog
    </button>
  </div>
  <Transition appear @enter="enterAnimaHandler">
    <div
      v-show="diaLogInfo.show"
      class="w-screen flex dark:bg-gray-950 dark:bg-opacity-50 dark:text-white h-screen justify-center items-center gap-5 flex-col fixed top-0 left-0 bg-opacity-50 backdrop-blur-md bg-white z-50"
    >
      <div
        ref="port"
        id="port"
        class="p-10 bg-opacity-25 flex justify-center items-center hover:border-orange-400 transition-all border h-1/2 bg-red-100 rounded-full w-1/2 overflow-hidden"
      ></div>
      <h1
        class="text-3xl dark:hover:bg-gray-700 hover:bg-gray-100 py-2 px-4 rounded-md transition-all duration-150"
      >
        I'm not Mario. I'm just a passing plumber
      </h1>
      <button
        @click="closeDialog"
        class="py-2 px-4 min-w-[100px] hover:bg-gray-100 hover:text-orange-500 transition-all duration-150 border rounded-full"
      >
        Exit
      </button>
    </div>
  </Transition>

  <div
    class="h-screen gap-5 w-screen grid p-5 overflow-hidden grid-cols-2 dark:bg-gray-900"
  >
    <div
      ref="boxs"
      class="h-full transition-all duration-200 gap-5 w-full bg-blue-700 rounded-2xl p-5 grid grid-cols-2"
    >
      <div
        @click="toBack"
        ref="box1"
        class="w-full h-full bg-gray-100 rounded-xl p-4 flex flex-col gap-2"
      >
        <div class="w-full h-10 bg-blue-800 rounded-xl"></div>
        <div class="w-2/3 h-10 bg-blue-800 rounded-xl"></div>
      </div>
      <div class="w-full h-full bg-gray-100 rounded-xl"></div>
      <div class="w-full h-full bg-gray-100 rounded-xl"></div>
      <div class="w-full h-full bg-gray-100 rounded-xl"></div>
      <div class="w-full h-full bg-gray-100 rounded-xl"></div>
      <div
        class="w-full h-full bg-red-400 rounded-xl"
        @click="sendTOCard"
      ></div>
    </div>
    <div
      ref="prop2"
      class="w-full bg-red-400 h-full p-5 grid grid-cols-2 gap-5 rounded-2xl"
    >
      <div class="w-full h-full bg-gray-100 rounded-xl"></div>
      <div class="w-full h-full bg-gray-100 rounded-xl"></div>
      <div class="w-full h-full bg-gray-100 rounded-xl"></div>
    </div>
  </div>
</template>
<script lang="ts" setup>
import img from "@/assets/imgs/mliao.png";
import gsap from "gsap";
import Flip from "gsap/Flip";
gsap.registerPlugin(Flip);
const demos = ref<HTMLElement | null>(null);
onMounted(() => {
  gsap.from(demos.value!.children, {
    x: "-40",
    stagger: 0.1,
    duration: 0.5,
    yoyo: true,
    repeat: -1,
    autoAlpha: 0,
  });
});
const port = ref<HTMLElement | null>(null);
const box = ref<HTMLElement | null>(null);

const diaLogInfo = reactive({
  show: false,
});

const openDialog = () => {
  diaLogInfo.show = true;
  const state = Flip.getState(box.value);
};

const closeDialog = () => {
  diaLogInfo.show = false;
};

const enterAnimaHandler = (e: HTMLElement): void => {
  gsap.from(e, {
    autoAlpha: 0,
    scale: 0,
  });
};
const box1 = ref<HTMLElement | null>(null);
const boxs = ref<HTMLElement | null>(null);
const prop2 = ref<HTMLElement | null>(null);
const sendTOCard = () => {
  const state = Flip.getState([prop2.value, box1.value, boxs.value]);
  prop2.value!.appendChild(box1.value!);
  Flip.from(state, { duration: 1, scale: true });
};

const toBack = () => {
  const state = Flip.getState([prop2.value, box1.value, boxs.value]);
  boxs.value!.append(box1.value!);
  Flip.from(state, { duration: 1, scale: true });
};
</script>

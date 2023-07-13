<template>
  <div class="w-screen h-screen dark:bg-gray-900 overflow-hidden">
    <div
      class="flex h-full dark:bg-gray-900 dark:text-white items-center justify-center container"
    >
      <div class="box">
        <p>You</p>
        <b class="px-2 py-1 rounded-sm">Tube</b>
        <button
          @click="navigateTo('/filp')"
          class="border ml-2 py-1 px-2 rounded-md"
        >
          GoTo -> Filp
        </button>
      </div>
    </div>
  </div>
</template>

<script lang="ts" setup>
import gsap from "gsap";
import ScrollTrigger from "gsap/ScrollTrigger";
const top = ref();
gsap.registerPlugin(ScrollTrigger);

// onMounted(() => {
//   let tl = gsap.timeline({
//     scrollTrigger: {
//       trigger: ".container",
//       pin: true,
//       start: "top top",
//       end: "+=500",
//       scrub: 1,
//       snap: {
//         snapTo: "labels",
//         duration: { min: 0.2, max: 3 },
//         delay: 0.2,
//         ease: "power1.inOut",
//       },
//     },
//   });

//   tl.addLabel("start")
//     .from(".box p", { scale: 0, autoAlpha: 0 })
//     .addLabel("start")
//     .from(".box b", { scale: 0, autoAlpha: 0 })
//     .addLabel("spin")
//     .to(".box", { scale: 6 })
//     .to(".box b", { scale: 6, background: "red", color: "white" })
//     .addLabel("end");
// });
</script>

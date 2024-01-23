<script setup>
import { onClickOutside } from "@vueuse/core";
import { onMounted, ref } from "vue";
import FacebookIcon from "./components/Facebook.vue";
import InstagramIcon from "./components/Instagram.vue";
import PlusIcon from "./components/Plus.vue";

const isModalOpen = ref(false);
const modal = ref(null);
onClickOutside(modal, () => (isModalOpen.value = false));

const loaded = ref(false);
onMounted(() => {
  setTimeout(() => (loaded.value = true), 1500);
});

const bgImage = new URL("./assets/background.webp", import.meta.url).href;
</script>

<template>
  <div
    class="relative isolate flex min-h-screen w-auto flex-col overflow-hidden font-display"
  >
    <img
      :src="bgImage"
      alt="background image of a forest withe the sun shining through the trees"
      class="inset-0 -z-10 w-full scale-150 object-scale-down md:absolute md:h-full md:transform-none md:object-cover"
    />

    <div id="modal"></div>
    <div
      class="flex grow flex-col bg-[#611818] md:min-h-screen md:max-w-sm md:justify-end"
    >
      <div
        class="font-serif mx-4 mt-12 md:ml-36 md:w-screen md:overflow-visible"
      >
        <div class="flex flex-col gap-y-8 md:gap-y-1">
          <Transition
            name="fade"
            enter-from-class="opacity-0"
            enter-to-class="opacity-100"
            enter-active-class="transition ease-out duration-1000"
          >
            <h1
              v-show="loaded"
              class="text-center text-7xl font-bold text-white md:text-left md:text-9xl"
            >
              Explore
            </h1>
          </Transition>
          <div class="flex items-center justify-center md:justify-start">
            <button
              type="button"
              @click="isModalOpen = true"
              class="inline-flex items-center gap-x-2 p-3 text-xl text-white focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-white md:gap-x-5 md:bg-transparent"
            >
              <PlusIcon class="h-10 w-10 rounded-full bg-[#611818] p-0.5" />
              More Details
            </button>
          </div>
        </div>
        <div class="mb-6 mt-16 flex justify-center md:mr-36 md:justify-end">
          <div class="flex gap-x-6 md:mr-6 md:flex-col md:gap-y-4">
            <FacebookIcon class="h-16 w-16 text-white" />
            <InstagramIcon class="h-16 w-16 text-white" />
          </div>
        </div>
      </div>
    </div>
  </div>
  <Teleport to="#modal">
    <Transition
      name="modal"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      enter-active-class="transition ease-out duration-300"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
      leave-active-class="transition ease-in duration-300"
    >
      <div
        v-if="isModalOpen"
        class="fixed z-50 mx-2 h-fit max-h-fit max-w-full bg-white px-4 pb-24 pt-2 md:my-48 md:ml-36 md:w-7/12 md:px-12 lg:w-5/12"
      >
        <div ref="modal" class="flex justify-end">
          <button @click="isModalOpen = false" class="text-3xl text-[#611818]">
            x
          </button>
        </div>
        <div class="flex flex-col gap-y-4 pt-2 md:gap-y-8 md:pt-8">
          <h3 class="text-6xl text-[#611818] md:text-7xl">Explore</h3>
          <p class="text-xs md:text-sm">
            We must be quiet, soft and gentle. The man who does the best job is
            the one who is happy at his job. These little son of a guns hide in
            your brush and you just have to push them out. We'll put all the
            little clouds in and let them dance around and have fun. Maybe
            there's a little something happening right here. I started painting
            as a hobby when I was little. I didn't know I had any talent. I
            believe talent is just a pursued interest. Anybody can do what I do.
            Everyone is going to see things differently - and that's the way it
            should be. I guess I'm a little weird. I like to talk to trees and
            animals. That's okay though; I have more fun than most people. You
            are only limited by your imagination. You can't make a mistake.
            Anything that happens you can learn to use - and make something
            beautiful out of it.
          </p>
          <button
            class="w-fit bg-gradient-to-r from-[#611818] to-[#9F6452] px-12 py-4 font-semibold uppercase text-white"
          >
            Read More
          </button>
        </div>
      </div>
    </Transition>
  </Teleport>
</template>

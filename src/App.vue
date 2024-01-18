<script setup>
import { onClickOutside } from "@vueuse/core";
import { ref } from "vue";
import FacebookIcon from "./components/Facebook.vue";
import InstagramIcon from "./components/Instagram.vue";
import PlusIcon from "./components/Plus.vue";
const isModalOpen = ref(false);
const modal = ref(null);
onClickOutside(modal, () => (isModalOpen.value = false));
const bgImage = new URL("./assets/background.webp", import.meta.url).href;
let bgColor = "#611818";
</script>

<template>
    <div class="relative isolate overflow-hidden min-h-screen min-w-screen">
        <img
            :src="bgImage"
            alt=""
            class="absolute inset-0 -z-10 h-full w-full object-cover"
        />
        <div
            class="max-w-sm bg-[#611818] min-h-screen flex flex-col justify-end"
        >
            <div class="ml-36 w-screen font-serif overflow-visible">
                <div id="modal"></div>
                <h1 class="text-9xl font-bold text-white">Explore</h1>
                <div class="flex items-center">
                    <button
                        type="button"
                        @click="isModalOpen = true"
                        class="inline-flex items-center gap-x-5 text-xl text-white  focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-white"
                    >
                        <PlusIcon class="w-10 h-10" />
                        More Details
                    </button>
                </div>
                <div
                    class="mt-16 mb-6 mr-36 flex flex-row justify-end max-w-full"
                >
                    <div class="flex flex-col gap-y-4 mr-4">
                        <FacebookIcon class="w-16 h-16 text-white" />
                        <InstagramIcon class="w-16 h-16 text-white" />
                    </div>
                </div>
            </div>
        </div>
    </div>
    <Teleport to="#modal">
        <div v-if="isModalOpen" class="">
            <div ref="modal">
                <button @click="isModalOpen = false">Close</button>
                This is the Modal!
            </div>
        </div>
    </Teleport>
</template>

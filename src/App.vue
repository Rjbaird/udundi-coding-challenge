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
    <div
        class="relative isolate overflow-hidden min-h-screen min-w-screen flex flex-col"
    >
        <img
            :src="bgImage"
            alt="background image of a forest withe the sun shining through the trees"
            class="md:absolute -z-10 scale-150 md:transform-none md:h-full w-full object-scale-down md:object-cover inset-0"
        />
        <div
            class="md:max-w-sm bg-[#611818] md:min-h-screen flex flex-col md:justify-end grow"
        >
            <div
                class="mx-4 mt-12 md:ml-36 md:w-screen font-serif md:overflow-visible"
            >
                <div class="flex flex-col gap-y-8 md:gap-y-1">
                    <div id="modal"></div>
                    <h1
                        class="text-7xl md:text-9xl font-bold text-white text-center md:text-left"
                    >
                        Explore
                    </h1>
                    <div
                        class="flex justify-center items-center md:justify-start"
                    >
                        <button
                            type="button"
                            @click="isModalOpen = true"
                            class="inline-flex items-center p-3 gap-x-2 md:gap-x-5 rounded-full md:rounded-none text-xl text-[#611818] md:text-white bg-white md:bg-transparent focus-visible:outline focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-white"
                        >
                            <PlusIcon
                                class="w-10 h-10 bg-[#611818] rounded-full p-0.5"
                            />
                            More Details
                        </button>
                    </div>
                </div>
                <div
                    class="mt-16 mb-6 md:mr-36 flex justify-center md:justify-end"
                >
                    <div class="flex md:flex-col gap-x-6 md:gap-y-4 md:mr-6">
                        <FacebookIcon class="w-16 h-16 text-white" />
                        <InstagramIcon class="w-16 h-16 text-white" />
                    </div>
                </div>
            </div>
        </div>
    </div>
    <Teleport to="#modal">
        <div
            v-if="isModalOpen"
            class="text-center fixed z-50 justify-center items-center w-full h-[calc(100%-1rem)] max-h-60 bg-white p-4 m-4"
        >
            <div ref="modal">
                <button @click="isModalOpen = false">Close</button>
                This is the Modal!
            </div>
        </div>
    </Teleport>
</template>

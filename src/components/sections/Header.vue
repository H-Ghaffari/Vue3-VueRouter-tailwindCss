<template>
    <header>
        <nav class="py-2 px-3 bg-gray-100 flex flex-col md:flex-row md:items-center md:gap-x-14">
            <div class="flex items-center justify-between">
                <a href="#" class="inline-block text-xl">Ghaffari</a>
                <button @click="showHeader()"
                    class="border p-1.5 border-gray-800 rounded md:hidden focus:ring-4 focus:ring-gray-700">
                    <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 24 24" fill="currentColor" class="w-6 h-6">
                        <path fill-rule="evenodd"
                            d="M3 6.75A.75.75 0 013.75 6h16.5a.75.75 0 010 1.5H3.75A.75.75 0 013 6.75zM3 12a.75.75 0 01.75-.75h16.5a.75.75 0 010 1.5H3.75A.75.75 0 013 12zm0 5.25a.75.75 0 01.75-.75h16.5a.75.75 0 010 1.5H3.75a.75.75 0 01-.75-.75z"
                            clip-rule="evenodd" />
                    </svg>
                </button>
            </div>

            <div ref="ulRef" class="transition-all duration-500 max-h-0 md:max-h-none overflow-hidden">
                <ul class="flex flex-col md:flex-row gap-y-2.5 md:gap-x-5 md:gap-y-0 text-gray-600">
                    <li>
                        <router-link to="/" class="block p-2 cursor-pointer hover:text-gray-800 ">Home</router-link>
                    </li>
                    <li>
                        <router-link to="/users" class="block p-2 cursor-pointer hover:text-gray-800">Users</router-link>
                    </li>
                    <li>
                        <router-link to="/posts" class="block p-2 cursor-pointer hover:text-gray-800 ">Posts</router-link>
                    </li>
                </ul>
            </div>

        </nav>
    </header>
</template>

<script setup>
import { ref } from 'vue'
const ulRef = ref(null);
let ulShow = ref(false);
function showHeader() {
    ulShow.value = !ulShow.value;
    if (ulShow.value) {
        ulRef.value.classList.remove('max-h-0');
        ulRef.value.classList.add('max-h-[400px]');
    } else {
        ulRef.value.classList.remove('max-h-[400px]');
        ulRef.value.classList.add('max-h-0');
    }
}
</script>

<style scoped>
.router-link-active {
    @apply text-black text-opacity-90 border-b-2 border-b-black border-opacity-90
}
</style>
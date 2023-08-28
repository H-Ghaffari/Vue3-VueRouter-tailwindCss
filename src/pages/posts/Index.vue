<template>
    <div class="container mx-auto px-4 m-10">
        <RouterLink :to="{ name: 'postCreate' }"
            class="px-3.5 transition-all inline-block py-1.5 mb-6 rounded-md hover:opacity-70 bg-black text-white">
            Create
            Post
        </RouterLink>
        <div v-if="loading"
            class="w-8 h-8 mx-auto rounded-full animate-spin border-4 border-solid border-black border-t-transparent">
        </div>
        <div v-else class="grid grid-cols-12 gap-4">
            <div v-for="post in posts" :key="post.id" class="col-span-12 sm:col-span-6 lg:col-span-4 xl:col-span-3">
                <div class="border border-gray-300 pb-2 rounded-md w-full overflow-hidden">
                    <router-link :to="{ name: 'postId', params: { id: post.id } }"
                        class="block text-blue-600 underline cursor-pointer hover:text-blue-800 mb-2 bg-gray-100 bg-opacity-70 px-4 border-b pb-2 pt-2 border-gray-400">
                        {{
                            post.title
                        }}
                    </router-link>
                    <div class="block px-4">{{ post.body }}</div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import axios from 'axios';
import { ref } from 'vue';

const posts = ref([]);
const loading = ref(true);

function getPosts() {
    loading.value = true;
    axios.get('https://jsonplaceholder.typicode.com/posts')
        .then(function (response) {
            posts.value = response.data;
        })
        .catch(function (error) {
            console.log(error);
        })
        .finally(function () {
            loading.value = false;
        });
}
getPosts();

</script>

<style scoped></style>

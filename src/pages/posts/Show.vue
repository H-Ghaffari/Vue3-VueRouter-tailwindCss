<template>
    <div class="container mx-auto px-6 m-10">
        <div v-if="loading"
            class="w-8 h-8 mx-auto rounded-full animate-spin border-4 border-solid border-black border-t-transparent">
        </div>
        <div v-else class="grid grid-cols-12">
            <div class="col-span-12 sm:col-span-10 md:col-span-8 lg:col-span-6 xl:col-span-5">
                <div class="border border-gray-300 rounded-md w-full overflow-hidden">
                    <div class="block mb-2 bg-gray-100 bg-opacity-70 px-4 border-b pb-2 pt-2 border-gray-400">
                        {{
                            post.title
                        }}
                    </div>
                    <div class="block px-4 border-b pb-2 border-gray-400">
                        {{ post.body }}
                    </div>
                    <div class="flex gap-x-6 py-2 px-4 bg-gray-100">
                        <button @click="deletePost()" :disabled="deleteLoading"
                            class="flex transition-all items-center px-2.5 py-1 text-sm rounded hover:bg-red-800 bg-red-600 text-white">
                            <div v-if="deleteLoading"
                                class="w-3 h-3 mx-auto rounded-full animate-spin border-2 mr-2 border-solid border-white border-t-transparent">
                            </div>
                            <span>Delete</span>
                        </button>
                        <RouterLink :to="{ name: 'postEdit', params: { id: route.params.id } }"
                            class="px-2.5 transition-all text-sm inline-block py-1 rounded hover:opacity-70 bg-black text-white">
                            Edit
                        </RouterLink>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<script setup>
import axios from 'axios';
import { ref } from 'vue';
import {useRoute}  from 'vue-router'
import Swal from "sweetalert2";

const post = ref({});
const loading = ref(true);
const route = useRoute();
const deleteLoading= ref(false);

function getPost() {
    loading.value = true;
    axios.get(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
        .then(function (response) {
            post.value = response.data;
        })
        .catch(function (error) {
            console.log(error);
        })
        .finally(function () {
            loading.value = false;
        });
}
getPost();

function deletePost() {
    deleteLoading.value=true;
         axios.delete(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
        .then(function () {
            Swal.fire({
                title: "Thanks!",
                text: `Post (${route.params.id}) deleted successfully`,
                icon: "info",
                confirmButtonText: "Ok",
                padding: "0px 0px 10px 0px",
                width: '300px',
                position: 'top',
                iconColor: '#f07f07',
                confirmButtonColor: '#3975ed'
            });
        })
        .catch(function (error) {
            console.log(error);
        }).finally(function () {
             deleteLoading.value=false;
        });
}

</script>

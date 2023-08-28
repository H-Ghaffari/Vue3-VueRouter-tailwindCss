<template>
    <div class="container mx-auto px-4 m-10">
        <div v-if="loading"
            class="w-8 h-8 mx-auto rounded-full animate-spin border-4 border-solid border-black border-t-transparent">
        </div>
        <div v-else class="grid grid-cols-12 gap-4">
            <div v-for="user in users" :key="user.id" class="col-span-12 sm:col-span-6 lg:col-span-4 xl:col-span-3">
                <Card :user="user"></Card>
            </div>
        </div>
    </div>
</template>

<script setup>
import axios from 'axios';
import { ref } from 'vue';
// import Card from '@/components/users/Card.vue' //@=src
import Card from '../../components/users/Card.vue'

const users = ref([]);
const loading = ref(true);

function getUsers() {
    loading.value = true;
    axios.get('https://jsonplaceholder.typicode.com/users')
        .then(function (response) {
            // handle success
            // console.log(response.data);
            users.value = response.data;
        })
        .catch(function (error) {
            // handle error
            console.log(error);
        })
        .finally(function () {
            // always executed
            loading.value = false;
        });
}
getUsers();

</script>

<style scoped></style>

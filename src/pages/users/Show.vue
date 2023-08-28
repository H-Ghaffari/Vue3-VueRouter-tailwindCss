<template>
    <div class="container mx-auto px-6 m-10">
        <div v-if="loading"
            class="w-8 h-8 mx-auto rounded-full animate-spin border-4 border-solid border-black border-t-transparent">
        </div>
        <div v-else class="grid grid-cols-12 gap-4">
            <div class="col-span-12 sm:col-span-6 lg:col-span-4 xl:col-span-3">
                <Card :user="user"></Card>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<script setup>
import axios from 'axios';
import { ref } from 'vue';
import Card from '../../components/users/Card.vue'
import {useRoute}  from 'vue-router'

const user = ref({});
const loading = ref(true);
const route = useRoute();

function getUser() {
    loading.value = true;
    axios.get(`https://jsonplaceholder.typicode.com/users/${route.params.id}`)
        .then(function (response) {
            // handle success
            // console.log(response.data);
            user.value = response.data;
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
getUser();

</script>

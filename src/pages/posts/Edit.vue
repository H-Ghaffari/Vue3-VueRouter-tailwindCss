<template>
    <div class="container mx-auto px-4 m-10">
        <div v-if="loadingForm"
            class="w-8 h-8 mx-auto rounded-full animate-spin border-4 border-solid border-black border-t-transparent">
        </div>
        <Form v-else :loading="loading" @getFormData="editPost" :data="post" btnText="Edit Post" />
    </div>
</template>

<script setup>

import axios from "axios";
import Swal from "sweetalert2";
import { ref } from "vue";
import Form from '../../components/posts/Form.vue'
import { useRoute } from 'vue-router'

const post = ref({});
const route = useRoute();

const loadingForm = ref(true);
const loading = ref(false);

function getPost() {
    loadingForm.value = true;
    axios.get(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`)
        .then(function (response) {
            post.value = response.data;
        })
        .catch(function (error) {
            console.log(error);
        })
        .finally(function () {
            loadingForm.value = false;
        });
}
getPost();

function editPost(form) {
    loading.value = true;
    axios.put(`https://jsonplaceholder.typicode.com/posts/${route.params.id}`, {
        title: form.title,
        body: form.bady,
        userId: 1,
    })
        .then(function () {
            Swal.fire({
                title: "Thanks!",
                text: "Post update successfully",
                icon: "success",
                confirmButtonText: "Ok",
                padding: "0px 0px 10px 0px",
                width: '300px',
                position: 'top',
                iconColor: '#14db38',
                confirmButtonColor: '#3975ed'
            });
        })
        .catch(function (error) {
            console.log(error);
        }).finally(function () {
            loading.value = false;
        });
}

</script>

<style scoped></style>
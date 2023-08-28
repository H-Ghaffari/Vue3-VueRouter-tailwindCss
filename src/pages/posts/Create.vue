<template>
    <div class="container mx-auto px-4 m-10">
        <Form :loading="loading" @getFormData="createPost" btnText="Create Post" />
    </div>
</template>

<script setup>

import axios from "axios";
import Swal from "sweetalert2";
import { ref } from "vue";
import Form from '../../components/posts/Form.vue'


const loading = ref(false);

function createPost(form) {
    loading.value = true;
    axios
        .post("https://jsonplaceholder.typicode.com/posts", {
            title: form.title,
            body: form.bady,
            userId: 1,
        })
        .then(function () {
            Swal.fire({
                title: "Thanks!",
                text: "Post created successfully",
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
<template>
    <form @submit.prevent="validate">
        <div class="grid grid-cols-12">
            <h1 class="text-3xl mb-10 sm:col-start-2 col-span-11 ">{{ btnText }} :</h1>
            <div class="mb-5 col-span-12 sm:col-start-2 sm:col-span-10 lg:w-[70%] xl:w-[60%]">
                <label for="title" class="inline-block mb-2">Title</label>
                <input type="text" id="title" v-model.lazy.trim="form.title"
                    class="w-full border rounded px-3 py-1.5 border-gray-300 focus:outline-none focus:ring-4 focus:ring-blue-300 focus:ring-opacity-80 focus:border-blue-400">
                <span class="text-sm text-red-500"> {{ form.titleErrorText }}</span>
            </div>
            <div class="col-span-12 mb-5 sm:col-start-2 sm:col-span-10 lg:w-[70%] xl:w-[60%]">
                <label for="body" class="inline-block mb-2">Body</label>
                <textarea id="body" rows="5" v-model.lazy.trim="form.body"
                    class="w-full border rounded px-3 py-1.5 border-gray-300 focus:outline-none focus:ring-4 focus:ring-blue-300 focus:ring-opacity-80 focus:border-blue-400"></textarea>
                <span class="text-sm text-red-500"> {{ form.bodyErrorText }}</span>
            </div>
            <div class="col-span-12 sm:col-start-2 sm:col-span-10 lg:w-[70%] xl:w-[60%]">
                <button :disabled="loading"
                    class="px-3.5 flex items-center py-1.5 mb-6 rounded-md hover:opacity-70 bg-black text-white">
                    <div v-if="loading"
                        class="w-4 h-4 mx-auto rounded-full animate-spin border-2 mr-2 border-solid border-white border-t-transparent">
                    </div>
                    <span>{{ btnText }}</span>
                </button>
            </div>
        </div>
    </form>
</template>

<script setup>
import { reactive } from "vue";

const props = defineProps({
    loading: Boolean,
    data: {
        type: Object,
        default: null
    },
    btnText: String
})
const emits = defineEmits(['getFormData']);

const form = reactive({
    title: props.data ? props.data.title : '',
    titleErrorText: "",
    body: props.data ? props.data.body : '',
    bodyErrorText: "",
});

function validate() {
    if (form.title === "") {
        form.titleErrorText = "Title is required";
    } else {
        form.titleErrorText = "";
    }
    if (form.body === "") {
        form.bodyErrorText = "Body is required";
    } else {
        form.bodyErrorText = "";
    }

    if (form.title !== "" && form.body !== "") {
        emits('getFormData', form);
    }
}
</script>

<style scoped></style>
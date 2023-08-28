<template>
    <div class="border border-gray-300 pb-2 rounded-md w-full overflow-hidden">
        <router-link :to="{ name: 'userId', params: { id: user.id } }"
            class="block text-blue-600 underline cursor-pointer hover:text-blue-800 mb-2 bg-gray-100 bg-opacity-70 px-4 border-b pb-2 pt-2 border-gray-400">
            {{
                user.name
            }}
        </router-link>
        <div class="block mb-2 px-4 border-b pb-2 border-gray-400">Username : {{ user.username }}</div>
        <div class="block mb-2 px-4 border-b pb-2 border-gray-400">Email : {{ user.email }}</div>
        <div class="block px-4">Phone :{{ user.phone }}</div>
    </div>
</template>

<script setup>
const props = defineProps({
    user: Object
})
</script>

<style scoped></style>
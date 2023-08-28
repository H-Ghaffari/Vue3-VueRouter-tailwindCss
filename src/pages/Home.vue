<template>
    <div class="container mx-auto mt-10 md:grid md:grid-cols-12 px-4">
        <div class="md:col-span-6">
            <p>Lorem ipsum dolor sit amet consectetur adipisicing elit. Dolorem totam, ratione, voluptas eveniet soluta
                incidunt
                itaque optio beatae id temporibus, ex exercitationem sint ad earum in sed? Quam, cum sunt. Lorem ipsum dolor
                sit
                amet consectetur adipisicing elit. Dolorem totam, ratione, voluptas eveniet soluta incidunt itaque optio
                beatae
                id temporibus, ex exercitationem sint ad earum in sed? Quam, cum sunt.
            </p>
            <div class="flex gap-x-4 mt-6">
                <RouterLink to="/users"
                    class="px-3.5 transition-all py-1.5 rounded-md hover:opacity-70 bg-black text-white">Users
                </RouterLink>
                <RouterLink to="/posts" class="px-3.5 transition-all py-1.5 rounded-md hover:bg-gray-300 bg-gray-100">Posts
                </RouterLink>
            </div>
        </div>
    </div>
</template>

<script setup>

</script>

<style  scoped></style>
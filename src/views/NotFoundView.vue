<script setup>
import { RouterLink } from 'vue-router';
</script>

<template>
    <div class="container mx-auto py-16 text-center">
        <i class="pi pi-exclamation-triangle  text-orange-500 text-7xl pb-8"></i>
        <h1 class="text-4xl font-bold text-center text-gray-700">404 - Not Found</h1>
        <p class="text-md text-center text-gray-500">
            The page you are looking for could not be found.
        </p>
        <div class="text-center mt-8">
            <RouterLink to="/" class="bg-gray-600 hover:bg-gray-700 text-white py-2 px-4 rounded">
                Go Back Home
            </RouterLink>
        </div>
    </div>
</template>
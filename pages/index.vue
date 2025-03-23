<template>
  <div class="min-h-screen bg-gray-50 p-6">
    <div class="max-w-3xl mx-auto">
      <h1 class="text-4xl font-bold text-gray-800 mb-8 text-center">📝 Blog Posts</h1>

      <div v-if="status === 'pending'" class="text-center text-blue-600 font-medium">
        Loading posts...
      </div>

      <div v-else-if="status === 'error'" class="text-center text-red-500 font-semibold">
        Failed to load posts
      </div>

      <div v-else class="space-y-6">
        <NuxtLink class="block" v-for="post in posts" :key="post.id" :to="`/post/${post.id}`">
          <Post :post/>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const {data: posts, status} = await useFetch('https://jsonplaceholder.typicode.com/posts')
</script>

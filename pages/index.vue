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
        <NuxtLink
            v-for="post in posts"
            :key="post.id"
            :to="`/post/${post.id}`"
            class="block bg-white shadow-md rounded-2xl p-6 hover:shadow-lg transition"
        >
          <h2 class="text-2xl font-semibold text-gray-800 mb-2">
            {{ post.title }}
          </h2>
          <p class="text-gray-600 leading-relaxed line-clamp-3">
            {{ post.body }}
          </p>
        </NuxtLink>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const { data: posts, status } = await useFetch('https://jsonplaceholder.typicode.com/posts')
</script>

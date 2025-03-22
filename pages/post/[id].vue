<template>
  <div class="min-h-screen bg-white p-6">
    <div class="max-w-3xl mx-auto">
      <NuxtLink to="/" class="inline-block mb-6 text-blue-600 hover:underline">
        ← Back to Home
      </NuxtLink>

      <div v-if="status === 'pending'" class="text-center text-blue-600 font-medium">
        Loading post...
      </div>

      <div v-else-if="status === 'error'" class="text-center text-red-500 font-semibold">
        Failed to load post
      </div>

      <div v-else-if="post" class="bg-gray-50 p-8 rounded-2xl shadow-md">
        <h1 class="text-3xl font-bold text-gray-800 mb-4">{{ post.title }}</h1>
        <p class="text-gray-700 leading-relaxed">{{ post.body }}</p>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
const route = useRoute()
const postId = route.params.id

const { data: post, status } = await useFetch(
    `https://jsonplaceholder.typicode.com/posts/${postId}`,
    {
      onResponse({ response }) {
        if(!response.ok){
          showError({
            statusCode: 404,
            statusMessage: 'Post Not Found'
          })
        }
      },
    }
)

if (!post.value){
  throw createError({
    statusCode: 404,
    statusMessage: 'Post Not Found'
  })
}
</script>

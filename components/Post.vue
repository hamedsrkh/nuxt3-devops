<template>
  <div
      class="block bg-white shadow-md rounded-2xl p-6 hover:shadow-lg transition"
  >
    <h2 class="text-2xl font-semibold text-gray-800 mb-2">
      {{ post.title }}
    </h2>
    <p class="text-gray-600 leading-relaxed line-clamp-3">
      {{ post.body }}
    </p>
  </div>
</template>

<script setup lang="ts">
interface Post {
  title: string
  id: number
  body: string
}

defineProps<{
  post: Post
}>()
</script>

<style scoped>

</style>
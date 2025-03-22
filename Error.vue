<template>
  <div class="min-h-screen flex items-center justify-center bg-gray-100 text-gray-800">
    <div class="text-center max-w-xl p-8">
      <h1 class="text-6xl font-bold mb-4">
        {{ error?.statusCode || 500 }}
      </h1>
      <p class="text-2xl font-semibold mb-4">
        {{ title }}
      </p>
      <p class="text-gray-600 mb-6">
        {{ error?.message || 'Something went wrong.' }}
      </p>
      <NuxtLink to="/" class="inline-block bg-blue-600 text-white px-6 py-3 rounded-xl hover:bg-blue-700 transition">
        Go to Homepage
      </NuxtLink>
    </div>
  </div>
</template>

<script setup lang="ts">
import type { NuxtError } from '#app'

const props = defineProps({
  error: Object as () => NuxtError
})

const title = computed(() => {
  if (props.error?.statusCode === 404) return 'Page Not Found'
  if (props.error?.statusCode === 500) return 'Internal Server Error'
  return 'Oops! Something went wrong.'
})
</script>

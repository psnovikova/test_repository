<script setup>
import { CodeIcon, StarIcon } from '@heroicons/vue/outline'

defineProps({
  repository: {
    type: Object,
    required: true,
  },
})
</script>

<template>
  <a
    :href="repository.html_url" target="_blank"
    class="flex flex-col space-y-3 w-full hover:bg-white border border-transparent rounded-xl p-4 hover:shadow-md duration-200 dark:hover:bg-stone-700 dark:hover:border-stone-600"
  >
    <div class="flex flex-row items-center space-x-3">
      <img
        class="w-12 h-12 rounded-full bg-white ring ring-stone-200"
        :src="`https://avatars.githubusercontent.com/u/${repository.owner.id}?s=64`"
      >
      <div class="flex flex-col space-y-1">
        <div class="font-bold">
          {{ repository.full_name }}
        </div>
        <div class="flex flex-row items-center text-sm space-x-4">
          <div class="flex flex-row items-center">
            <CodeIcon class="w-4 h-4" />
            <span class="ml-1">
              {{ repository.language || '???' }}
            </span>
          </div>
          <div class="flex flex-row items-center">
            <StarIcon class="w-4 h-4" />
            <span class="ml-1">
              {{ repository.stargazers_count }}
            </span>
          </div>
        </div>
      </div>
    </div>
    <div v-if="repository.description" class="text-stone-500 dark:text-stone-400">
      {{ repository.description }}
    </div>
  </a>
</template>

<style scoped>

</style>

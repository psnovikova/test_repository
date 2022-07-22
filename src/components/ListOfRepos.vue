<script setup>
import { ref } from 'vue'
import { useVModels } from '@vueuse/core'
import CardOfRepository from './CardOfRepository.vue'

const props = defineProps({
  arrayOfRepos: {
    type: Array,
    default: () => [],
  },
})
</script>

<template>
  <div class="flex flex-col items-center h-full overflow-auto">
    <!--      карточка вывода запросов -->

    <CardOfRepository
      v-for="repo in arrayOfRepos"
      :key="repo.id"
      :repo="repo"
    />
  </div>
</template>

<style scoped>

</style>

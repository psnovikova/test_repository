<script setup>
import { ref, watch } from 'vue'
import { useDebounceFn } from '@vueuse/core'
import { UseDark } from '@vueuse/components'
import { MoonIcon, SunIcon } from '@heroicons/vue/outline'
import RepositoryCard from './components/RepositoryCard.vue'
import SearchBar from './components/SearchBar.vue'
import ThePaginate from './components/ThePaginate.vue'

const repositories = ref([])
const search = ref('')
const pageCount = ref(1)

const findRepositories = useDebounceFn(async (currentPage) => {
  const res = await fetch(`https://api.github.com/search/repositories?q=${search.value}&page=${currentPage}&per_page=10`)
  const data = await res.json()
  repositories.value = data.items
  pageCount.value = Math.ceil((data.total_count > 1000 ? 1000 : data.total_count) / 10)
  window.scrollTo(0, 0)
}, 300)

watch(search, () => {
  findRepositories(1)
})
</script>

<template>
  <div class="max-w-screen-md p-6 mx-auto mt-6 flex flex-col space-y-6">
    <div class="flex flex-row items-center">
      <h1 class="text-2xl font-semibold grow">
        Поиск по GitHub
      </h1>
      <UseDark v-slot="{ toggleDark }">
        <button
          class="flex flex-row items-center border rounded-xl bg-white px-4 py-2 space-x-3 shadow-sm dark:bg-stone-700 dark:border-stone-600"
          @click="toggleDark()"
        >
          <SunIcon class="w-6 h-6 dark:opacity-30" />
          <MoonIcon class="w-6 h-6 opacity-30 dark:opacity-100" />
        </button>
      </UseDark>
    </div>
    <SearchBar v-model="search" />
    <div class="flex flex-col items-center -mx-4">
      <div
        v-for="repository in repositories" :key="repository.id"
        class="w-full after:border-t after:grow after:block after:mt-3 after:pb-3 after:mx-4 dark:after:border-stone-600"
      >
        <RepositoryCard :repository="repository" />
      </div>
      <ThePaginate v-if="pageCount > 1" :page-count="pageCount" :click-handler="findRepositories" />
    </div>
  </div>
</template>

<style scoped>

</style>

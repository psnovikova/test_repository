<script setup>
import { computed, ref, watch } from 'vue'
import { useDebounceFn } from '@vueuse/core'
import { UseDark } from '@vueuse/components'
import { MoonIcon, SunIcon } from '@heroicons/vue/solid'
import SearchLine from './components/SearchLine.vue'
import ListOfRepos from './components/ListOfRepos.vue'
import Pagination from './components/Pagination.vue'

// для v-model in input
const search = ref('')

// для получения данных из fetch
const arrayOfRepos = ref([])

// для количества результатов поиска
const countOfRepos = ref(0)
const page = ref(1)
const perPage = 20
const maxPage = computed(() => {
  return Math.ceil(countOfRepos.value > 1000 ? 1000 / perPage : countOfRepos.value / perPage)
})

// debounce для ожидания ввода запроса
const searchReposFunc = useDebounceFn(async () => {
  let resFetch = null
  let data = null
  if (search.value) {
    resFetch = await fetch(`https://api.github.com/search/repositories?q=${search.value}&page=${page.value}&per_page=${perPage}`)
    data = await resFetch.json()
    countOfRepos.value = data.total_count
    arrayOfRepos.value = data.items
  }
}, 1000)

// отслеживание изменений в поиске
watch(search, () => {
  if (search.value) {
    page.value = 1
    searchReposFunc()
  }
  else {
    arrayOfRepos.value = []
    countOfRepos.value = 0
  }
})

watch(page, () => {
  searchReposFunc()
})
</script>

<template>
  <div class="w-screen h-screen flex flex-col">
    <UseDark v-slot="{ toggleDark }">
      <button
        class="bg-amber-200 dark:bg-stone-600 absolute right-10 top-8 w-24 h-10 rounded-xl"
        @click="toggleDark()"
      >
        <div class="flex justify-center space-x-6">
          <MoonIcon class="h-6 dark:opacity-100 opacity-20" />
          <SunIcon class="h-6 dark:opacity-20" />
        </div>
      </button>
    </UseDark>
    <SearchLine v-model="search" />
    <ListOfRepos :array-of-repos="arrayOfRepos" />
    <div v-if="maxPage" class="flex justify-center mt-5">
      <Pagination v-model="page" :max-page="maxPage" />
    </div>
  </div>
</template>

<style scoped>

</style>

<script setup>
import { ref } from 'vue'

// для получения данных из fetch
const array = ref()
// для v-model in input
const search = ref()

const searchFunc = async () => {
  setTimeout(async () => {
    const res = await fetch(`https://api.github.com/search/repositories?q=${search.value}&page=1&per_page=100`)
    const data = await res.json()
    array.value = data.items
  }, 2000)
}
</script>

<template>
  <div class="w-screen">
    <div class="flex justify-center mt-5 items-center">
      <!--      картинка с лупой -->
      <svg
        xmlns="http://www.w3.org/2000/svg"
        class="h-14 w-14 opacity-70 mr-3"
        viewBox="0 0 20 20" fill="currentColor"
      >
        <path fill-rule="evenodd" d="M8 4a4 4 0 100 8 4 4 0 000-8zM2 8a6 6 0 1110.89 3.476l4.817 4.817a1 1 0 01-1.414 1.414l-4.816-4.816A6 6 0 012 8z" clip-rule="evenodd" />
      </svg>
      <!--      ввод запроса -->
      <input
        v-model="search" placeholder="поиск..."
        class="border-2 border-slate-500 w-1/3 h-16 text-2xl pl-5"
        @input="searchFunc"
      >
    </div>
    <div class="flex flex-col items-center">
      <!--      карточка вывода запросов -->
      <div
        v-for="repos in array"
        :key="repos.id"
        class="flex mt-5 border-2 border-gray-600 pt-3 pb-3 pl-5 w-3/4 flex-col"
      >
        <div>
          Author: <a
            class="cursor-pointer text-fuchsia-800"
            :href="repos.owner.html_url"
          >
            {{ repos.owner.login }}
          </a>
        </div>
        <div>
          Repository: {{ repos.name }}
        </div>
        <div>
          Description: {{ repos.description }}
        </div>
        <div>
          Language: {{ repos.language }}
        </div>
        <div class="flex">
          Stars: {{ repos.stargazers_count }}
          <!--          картинка-звёздочка -->
          <svg
            xmlns="http://www.w3.org/2000/svg"
            class="h-5 w-5 ml-2 pt-1"
            viewBox="0 0 20 20"
            fill="orange"
            stroke="red"
          >
            <path d="M9.049 2.927c.3-.921 1.603-.921 1.902 0l1.07 3.292a1 1 0 00.95.69h3.462c.969 0 1.371 1.24.588 1.81l-2.8 2.034a1 1 0 00-.364 1.118l1.07 3.292c.3.921-.755 1.688-1.54 1.118l-2.8-2.034a1 1 0 00-1.175 0l-2.8 2.034c-.784.57-1.838-.197-1.539-1.118l1.07-3.292a1 1 0 00-.364-1.118L2.98 8.72c-.783-.57-.38-1.81.588-1.81h3.461a1 1 0 00.951-.69l1.07-3.292z" />
          </svg>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>

</style>

<script setup>
defineProps({
  repo: {
    type: Object,
    required: true,
  },
})
</script>

<template>
  <div
    class="flex mt-5 border-2 border-gray-600 pt-3 pb-3 pl-5 w-3/4 flex-col dark:border-neutral-500"
  >
    <div>
      Author: <a
        class="cursor-pointer text-fuchsia-800 dark:text-fuchsia-200"
        :href="repo.owner.html_url"
      >
        {{ repo.owner.login }}
      </a>
    </div>
    <div>
      Repository: <a
        class="cursor-pointer text-lime-600 dark:text-lime-200"
        :href="repo.html_url"
      >
        {{ repo.name }}
      </a>
    </div>
    <div>
      Description: {{ repo.description }}
    </div>
    <div>
      Language: {{ repo.language }}
    </div>
    <div class="flex">
      Stars: {{ repo.stargazers_count }}
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
</template>

<style scoped>

</style>

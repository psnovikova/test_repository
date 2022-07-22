<script setup>
import { ref } from 'vue'
import { useVModels } from '@vueuse/core'

const props = defineProps({
  modelValue: {
    type: String,
    required: true,
  },
})

const emits = defineEmits(['update:modelValue'])

const { modelValue: search } = useVModels(props, emits)
</script>

<template>
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
      class="border-2 border-slate-500 w-1/3 h-16 text-2xl pl-5 dark:bg-stone-600 outline-none rounded-lg border-neutral-800 dark:border-neutral-500"
    >
  </div>
</template>

<style scoped>

</style>

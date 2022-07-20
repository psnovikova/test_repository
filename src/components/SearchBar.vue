<script setup>
import { useVModel } from '@vueuse/core'
import { SearchIcon } from '@heroicons/vue/outline'
import { onMounted, ref } from 'vue'

const props = defineProps({
  modelValue: {
    type: String,
    required: true,
  },
})
const emit = defineEmits(['update:modelValue'])

const value = useVModel(props, 'modelValue', emit)
const input = ref()

onMounted(() => {
  input.value.focus()
})
</script>

<template>
  <div class="flex flex-row items-center border rounded-xl bg-white px-4 py-2 space-x-3 shadow-sm dark:bg-stone-700 dark:border-stone-600">
    <SearchIcon class="w-6 h-6 shrink-0" />
    <input
      ref="input"
      v-model="value"
      placeholder="Найти репозитории..."
      class="bg-transparent grow focus:outline-none dark:placeholder-stone-400"
    >
  </div>
</template>

<style scoped>

</style>

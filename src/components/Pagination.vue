<script setup>
import { ChevronLeftIcon, ChevronRightIcon } from '@heroicons/vue/solid'
import { useVModels } from '@vueuse/core'
import { watch } from 'vue'

const props = defineProps({
  maxPage: {
    type: Number,
    required: true,
  },
  modelValue: {
    type: Number,
    required: true,
  },
})

const emits = defineEmits(['update:modelValue'])

const { modelValue: page } = useVModels(props, emits)

watch(page, (newValue) => {
  if (newValue > props.maxPage)
    page.value = props.maxPage
})

const buttonLeft = () => {
  if (page.value > 1)
    page.value -= 1
}

const buttonRight = () => {
  if (page.value < props.maxPage)
    page.value += 1
}
</script>

<template>
  <div class="mb-5">
    <div
      class="flex border-neutral-800 dark:border-neutral-500 w-1/6 h-16 justify-between bottom-5 items-center"
    >
      <button
        :disabled="page === 1"
        class="disabled:cursor-not-allowed disabled:opacity-50"
        @click="buttonLeft"
      >
        <ChevronLeftIcon class="h-12" />
      </button>
      <input
        v-model="page"
        type="number"
        class="dark:bg-stone-600 w-20 h-10 text-2xl text-center -webkit-appearance: none;
"
      >
      <button
        :disabled="page === maxPage"
        class="disabled:cursor-not-allowed disabled:opacity-50"
        @click="buttonRight"
      >
        <ChevronRightIcon class="h-12" />
      </button>
    </div>
    <div class="w-full flex justify-center text-neutral-400">
      Страниц: {{ maxPage }}
    </div>
  </div>
</template>

<style scoped>
input::-webkit-outer-spin-button, input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}
</style>

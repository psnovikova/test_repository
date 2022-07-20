<script setup>
import Paginate from 'vuejs-paginate-next'

defineProps({
  pageCount: {
    type: Number,
    required: true,
  },
  clickHandler: {
    type: Function,
    required: true,
  },
})
</script>

<template>
  <Paginate
    :page-count="pageCount"
    :click-handler="clickHandler"
    prev-text="<"
    next-text=">"
    container-class="pg-c"
    page-link-class="pg-i"
    prev-link-class="pg-i"
    next-link-class="pg-i"
    no-li-surround
    hide-prev-next
  />
</template>

<style>
/*noinspection ALL*/
.pg-c {
  @apply flex items-center justify-center select-none shadow w-fit rounded-lg font-medium bg-white dark:bg-stone-600 divide-x dark:divide-stone-500
}
/*noinspection ALL*/
.pg-i {
  @apply first:rounded-l-lg last:rounded-r-lg py-1.5 px-3 sm:py-2 sm:px-4 cursor-pointer duration-200
}
/*noinspection ALL*/
.pg-i.disabled {
  @apply opacity-50 cursor-default
}
/*noinspection ALL*/
.pg-i.active {
  @apply bg-stone-200 dark:bg-stone-500
}
</style>

<template>
  <thead :class="theadClass">
    <slot></slot>
  </thead>
</template>

<script setup>
const props = defineProps({
  theadClass: {
    type: String,
    default: 'text-xs uppercase bg-gray-50 dark:bg-gray-800 border-b-2 border-gray-200 dark:border-gray-700'
  }
})
</script>

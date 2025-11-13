<template>
  <tr :class="trClass">
    <slot></slot>
  </tr>
</template>

<script setup>
const props = defineProps({
  trClass: {
    type: String,
    default: 'bg-white dark:bg-gray-900 hover:bg-gray-50 dark:hover:bg-gray-800/50 transition-colors duration-150'
  }
})
</script>

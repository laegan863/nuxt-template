<template>
  <tbody :class="tbodyClass">
    <slot></slot>
  </tbody>
</template>

<script setup>
const props = defineProps({
  tbodyClass: {
    type: String,
    default: 'divide-y divide-gray-200 dark:divide-gray-700'
  }
})
</script>

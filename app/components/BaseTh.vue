<template>
  <th :class="thClass">
    <slot></slot>
  </th>
</template>

<script setup>
const props = defineProps({
  thClass: {
    type: String,
    default: 'px-6 py-4 font-semibold text-gray-700 dark:text-gray-300 tracking-wider'
  }
})
</script>

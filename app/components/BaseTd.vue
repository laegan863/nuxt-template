<template>
  <td :class="tdClass">
    <slot></slot>
  </td>
</template>

<script setup>
const props = defineProps({
  tdClass: {
    type: String,
    default: 'px-6 py-4 text-gray-900 dark:text-gray-100'
  }
})
</script>

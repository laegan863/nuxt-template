<template>
  <div :class="footerClass">
    <slot></slot>
  </div>
</template>

<script setup>
defineProps({
  footerClass: {
    type: String,
    default: 'flex items-center justify-end gap-3 p-6 border-t border-gray-200 dark:border-gray-700'
  }
})
</script>

<template>
  <div :class="bodyClass">
    <slot></slot>
  </div>
</template>

<script setup>
defineProps({
  bodyClass: {
    type: String,
    default: 'p-6'
  }
})
</script>

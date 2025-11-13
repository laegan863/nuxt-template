<template>
  <div class="flex items-center justify-between p-6 border-b border-gray-200 dark:border-gray-700">
    <div>
      <h3 v-if="title" class="text-xl font-bold text-gray-900 dark:text-white">
        {{ title }}
      </h3>
      <p v-if="subtitle" class="text-sm text-gray-500 dark:text-gray-400 mt-1">
        {{ subtitle }}
      </p>
      <slot></slot>
    </div>
    <button
      v-if="showClose"
      @click="$emit('close')"
      class="p-2 rounded-lg hover:bg-gray-100 dark:hover:bg-gray-700 text-gray-500 dark:text-gray-400 transition-colors"
    >
      <font-awesome-icon icon="times" class="text-lg" />
    </button>
  </div>
</template>

<script setup>
defineProps({
  title: {
    type: String,
    default: ''
  },
  subtitle: {
    type: String,
    default: ''
  },
  showClose: {
    type: Boolean,
    default: true
  }
})

defineEmits(['close'])
</script>

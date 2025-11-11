<template>
  <nav class="flex items-center space-x-2 text-sm mb-6">
    <NuxtLink 
      to="/dashboard" 
      class="text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors"
    >
      <font-awesome-icon icon="home" class="text-sm" />
    </NuxtLink>
    
    <template v-for="(item, index) in items" :key="index">
      <span class="text-gray-400 dark:text-gray-600">/</span>
      
      <NuxtLink 
        v-if="item.to && index < items.length - 1"
        :to="item.to"
        class="text-gray-500 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors"
      >
        {{ item.label }}
      </NuxtLink>
      
      <span 
        v-else
        class="text-gray-900 dark:text-white font-medium"
      >
        {{ item.label }}
      </span>
    </template>
  </nav>
</template>

<script setup>
defineProps({
  items: {
    type: Array,
    required: true,
    default: () => []
  }
})
</script>

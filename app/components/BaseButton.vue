<template>
  <button
    :type="type"
    :disabled="disabled || loading"
    class="inline-flex items-center justify-center font-medium rounded-lg transition-all duration-200 focus:outline-none focus:ring-2 focus:ring-offset-2 disabled:cursor-not-allowed disabled:opacity-60"
    :class="[
      sizeClasses,
      variantClasses,
      buttonClass,
      { 'gap-2': $slots.prefix || $slots.suffix || prefixIcon || suffixIcon || loading }
    ]"
    @click="$emit('click', $event)"
  >
    <!-- Loading Spinner -->
    <span v-if="loading" class="animate-spin">
      <font-awesome-icon icon="spinner" class="text-sm" />
    </span>
    
    <!-- Prefix Icon/Slot -->
    <span v-else-if="$slots.prefix || prefixIcon">
      <slot name="prefix">
        <font-awesome-icon v-if="prefixIcon" :icon="prefixIcon" class="text-sm" />
      </slot>
    </span>
    
    <!-- Button Content -->
    <slot>{{ label }}</slot>
    
    <!-- Suffix Icon/Slot -->
    <span v-if="!loading && ($slots.suffix || suffixIcon)">
      <slot name="suffix">
        <font-awesome-icon v-if="suffixIcon" :icon="suffixIcon" class="text-sm" />
      </slot>
    </span>
  </button>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  type: {
    type: String,
    default: 'button',
    validator: (value) => ['button', 'submit', 'reset'].includes(value)
  },
  variant: {
    type: String,
    default: 'primary',
    validator: (value) => ['primary', 'secondary', 'success', 'danger', 'warning', 'info', 'outline', 'ghost', 'link'].includes(value)
  },
  size: {
    type: String,
    default: 'md',
    validator: (value) => ['xs', 'sm', 'md', 'lg', 'xl'].includes(value)
  },
  label: {
    type: String,
    default: ''
  },
  disabled: {
    type: Boolean,
    default: false
  },
  loading: {
    type: Boolean,
    default: false
  },
  prefixIcon: {
    type: String,
    default: ''
  },
  suffixIcon: {
    type: String,
    default: ''
  },
  buttonClass: {
    type: String,
    default: ''
  },
  block: {
    type: Boolean,
    default: false
  }
})

defineEmits(['click'])

const sizeClasses = computed(() => {
  const sizes = {
    xs: 'px-2.5 py-1.5 text-xs',
    sm: 'px-3 py-2 text-sm',
    md: 'px-4 py-2.5 text-sm',
    lg: 'px-5 py-3 text-base',
    xl: 'px-6 py-3.5 text-base'
  }
  
  let classes = sizes[props.size] || sizes.md
  
  if (props.block) {
    classes += ' w-full'
  }
  
  return classes
})

const variantClasses = computed(() => {
  const variants = {
    primary: 'bg-blue-600 hover:bg-blue-700 text-white focus:ring-blue-500/50 shadow-sm',
    secondary: 'bg-gray-600 hover:bg-gray-700 text-white focus:ring-gray-500/50 shadow-sm',
    success: 'bg-green-600 hover:bg-green-700 text-white focus:ring-green-500/50 shadow-sm',
    danger: 'bg-red-600 hover:bg-red-700 text-white focus:ring-red-500/50 shadow-sm',
    warning: 'bg-yellow-500 hover:bg-yellow-600 text-white focus:ring-yellow-500/50 shadow-sm',
    info: 'bg-cyan-600 hover:bg-cyan-700 text-white focus:ring-cyan-500/50 shadow-sm',
    outline: 'bg-transparent border-2 border-gray-300 dark:border-gray-600 hover:bg-gray-50 dark:hover:bg-gray-800 text-gray-700 dark:text-gray-300 focus:ring-gray-500/50',
    ghost: 'bg-transparent hover:bg-gray-100 dark:hover:bg-gray-800 text-gray-700 dark:text-gray-300 focus:ring-gray-500/50',
    link: 'bg-transparent hover:underline text-blue-600 dark:text-blue-400 focus:ring-blue-500/50 shadow-none'
  }
  return variants[props.variant] || variants.primary
})
</script>

<template>
  <Transition
    enter-active-class="transition duration-300 ease-out"
    enter-from-class="transform translate-y-2 opacity-0"
    enter-to-class="transform translate-y-0 opacity-100"
    leave-active-class="transition duration-200 ease-in"
    leave-from-class="transform translate-y-0 opacity-100"
    leave-to-class="transform translate-y-2 opacity-0"
  >
    <div
      v-if="modelValue"
      class="rounded-xl border-2 p-4 transition-all duration-200"
      :class="alertClasses"
      role="alert"
    >
      <div class="flex items-start gap-3">
        <!-- Icon -->
        <div class="flex-shrink-0 mt-0.5">
          <font-awesome-icon :icon="iconName" class="text-lg" :class="iconColorClass" />
        </div>
        
        <!-- Content -->
        <div class="flex-1 min-w-0">
          <h4 v-if="title" class="font-semibold mb-1" :class="titleColorClass">
            {{ title }}
          </h4>
          <div class="text-sm" :class="textColorClass">
            <slot>{{ message }}</slot>
          </div>
        </div>
        
        <!-- Close Button -->
        <button
          v-if="dismissible"
          @click="close"
          class="flex-shrink-0 rounded-lg p-1.5 transition-colors duration-200 hover:bg-black/5 dark:hover:bg-white/5"
          :class="closeButtonClass"
        >
          <font-awesome-icon icon="times" class="text-sm" />
        </button>
      </div>
    </div>
  </Transition>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  modelValue: {
    type: Boolean,
    default: true
  },
  type: {
    type: String,
    default: 'info',
    validator: (value) => ['info', 'success', 'warning', 'error'].includes(value)
  },
  title: {
    type: String,
    default: ''
  },
  message: {
    type: String,
    default: ''
  },
  dismissible: {
    type: Boolean,
    default: true
  }
})

const emit = defineEmits(['update:modelValue', 'close'])

const iconName = computed(() => {
  const icons = {
    info: 'info-circle',
    success: 'check-circle',
    warning: 'exclamation-triangle',
    error: 'exclamation-circle'
  }
  return icons[props.type]
})

const alertClasses = computed(() => {
  const classes = {
    info: 'bg-blue-50 dark:bg-blue-950/20 border-blue-200 dark:border-blue-800',
    success: 'bg-green-50 dark:bg-green-950/20 border-green-200 dark:border-green-800',
    warning: 'bg-yellow-50 dark:bg-yellow-950/20 border-yellow-200 dark:border-yellow-800',
    error: 'bg-red-50 dark:bg-red-950/20 border-red-200 dark:border-red-800'
  }
  return classes[props.type]
})

const iconColorClass = computed(() => {
  const colors = {
    info: 'text-blue-600 dark:text-blue-400',
    success: 'text-green-600 dark:text-green-400',
    warning: 'text-yellow-600 dark:text-yellow-400',
    error: 'text-red-600 dark:text-red-400'
  }
  return colors[props.type]
})

const titleColorClass = computed(() => {
  const colors = {
    info: 'text-blue-900 dark:text-blue-300',
    success: 'text-green-900 dark:text-green-300',
    warning: 'text-yellow-900 dark:text-yellow-300',
    error: 'text-red-900 dark:text-red-300'
  }
  return colors[props.type]
})

const textColorClass = computed(() => {
  const colors = {
    info: 'text-blue-800 dark:text-blue-300',
    success: 'text-green-800 dark:text-green-300',
    warning: 'text-yellow-800 dark:text-yellow-300',
    error: 'text-red-800 dark:text-red-300'
  }
  return colors[props.type]
})

const closeButtonClass = computed(() => {
  const colors = {
    info: 'text-blue-600 dark:text-blue-400',
    success: 'text-green-600 dark:text-green-400',
    warning: 'text-yellow-600 dark:text-yellow-400',
    error: 'text-red-600 dark:text-red-400'
  }
  return colors[props.type]
})

const close = () => {
  emit('update:modelValue', false)
  emit('close')
}
</script>

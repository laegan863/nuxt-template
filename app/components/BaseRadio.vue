<template>
  <div class="flex items-start">
    <div class="flex items-center h-5">
      <input
        :id="radioId"
        type="radio"
        :name="name"
        :value="value"
        :checked="modelValue === value"
        @change="$emit('update:modelValue', value)"
        :disabled="disabled"
        :required="required"
        class="w-4 h-4 border transition-all duration-200 focus:ring-2 focus:ring-offset-0 cursor-pointer"
        :class="[
          radioClass,
          {
            'border-red-500 dark:border-red-400 focus:ring-red-500/20': error,
            'border-gray-300 dark:border-gray-600 text-blue-600 dark:text-blue-500 focus:ring-blue-500/20': !error && !disabled,
            'bg-gray-100 dark:bg-gray-900 border-gray-200 dark:border-gray-700 cursor-not-allowed': disabled
          }
        ]"
      />
    </div>
    <div v-if="label || $slots.default || hint || error" class="ml-3 text-sm">
      <label 
        :for="radioId" 
        class="font-medium cursor-pointer select-none"
        :class="labelClass || (error ? 'text-red-600 dark:text-red-400' : disabled ? 'text-gray-400 dark:text-gray-600 cursor-not-allowed' : 'text-gray-700 dark:text-gray-300')"
      >
        <slot>{{ label }}</slot>
        <span v-if="required" class="text-red-500 ml-0.5">*</span>
      </label>
      <p v-if="error" class="mt-1 text-xs text-red-600 dark:text-red-400">
        {{ error }}
      </p>
      <p v-else-if="hint" class="mt-1 text-xs text-gray-500 dark:text-gray-400">
        {{ hint }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  modelValue: {
    type: [String, Number, Boolean],
    required: true
  },
  value: {
    type: [String, Number, Boolean],
    required: true
  },
  name: {
    type: String,
    required: true
  },
  label: {
    type: String,
    default: ''
  },
  error: {
    type: String,
    default: ''
  },
  hint: {
    type: String,
    default: ''
  },
  disabled: {
    type: Boolean,
    default: false
  },
  required: {
    type: Boolean,
    default: false
  },
  radioClass: {
    type: String,
    default: ''
  },
  labelClass: {
    type: String,
    default: ''
  }
})

defineEmits(['update:modelValue'])

const radioId = computed(() => `radio-${Math.random().toString(36).substr(2, 9)}`)
</script>

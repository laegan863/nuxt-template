<template>
  <div class="w-full">
    <label 
      v-if="label" 
      :for="textareaId" 
      class="block text-sm font-medium mb-2"
      :class="labelClass || (error ? 'text-red-600 dark:text-red-400' : 'text-gray-700 dark:text-gray-300')"
    >
      {{ label }}
      <span v-if="required" class="text-red-500">*</span>
    </label>
    
    <div class="relative">
      <textarea
        :id="textareaId"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :placeholder="placeholder"
        :disabled="disabled"
        :readonly="readonly"
        :required="required"
        :rows="rows"
        :maxlength="maxlength"
        class="w-full px-4 py-2.5 text-sm rounded-lg border transition-all duration-200 focus:outline-none focus:ring-2"
        :class="[
          textareaClass,
          {
            'resize-none': !resizable,
            'resize-y': resizable,
            'border-red-500 dark:border-red-400 focus:ring-red-500/20': error,
            'border-gray-300 dark:border-gray-600 focus:ring-blue-500/20 focus:border-blue-500': !error && !disabled,
            'bg-gray-100 dark:bg-gray-800 text-gray-900 dark:text-gray-100': !disabled,
            'bg-gray-50 dark:bg-gray-900 text-gray-500 dark:text-gray-500 cursor-not-allowed': disabled,
            'bg-gray-50 dark:bg-gray-800': readonly
          }
        ]"
      ></textarea>
      
      <div 
        v-if="maxlength && showCount" 
        class="absolute bottom-2 right-2 text-xs px-2 py-1 rounded bg-gray-100 dark:bg-gray-700"
        :class="modelValue.length >= maxlength ? 'text-red-600 dark:text-red-400' : 'text-gray-500 dark:text-gray-400'"
      >
        {{ modelValue.length }} / {{ maxlength }}
      </div>
    </div>
    
    <p v-if="error" class="mt-1.5 text-xs text-red-600 dark:text-red-400">
      {{ error }}
    </p>
    <p v-else-if="hint" class="mt-1.5 text-xs text-gray-500 dark:text-gray-400">
      {{ hint }}
    </p>
  </div>
</template>

<script setup>
import { computed } from 'vue'

const props = defineProps({
  modelValue: {
    type: String,
    default: ''
  },
  label: {
    type: String,
    default: ''
  },
  placeholder: {
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
  readonly: {
    type: Boolean,
    default: false
  },
  required: {
    type: Boolean,
    default: false
  },
  rows: {
    type: Number,
    default: 4
  },
  maxlength: {
    type: Number,
    default: undefined
  },
  showCount: {
    type: Boolean,
    default: false
  },
  resizable: {
    type: Boolean,
    default: true
  },
  textareaClass: {
    type: String,
    default: ''
  },
  labelClass: {
    type: String,
    default: ''
  }
})

defineEmits(['update:modelValue'])

const textareaId = computed(() => `textarea-${Math.random().toString(36).substr(2, 9)}`)
</script>

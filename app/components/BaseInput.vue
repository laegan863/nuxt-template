<template>
  <div class="w-full">
    <label 
      v-if="label" 
      :for="inputId" 
      class="block text-sm font-medium mb-2"
      :class="labelClass || (error ? 'text-red-600 dark:text-red-400' : 'text-gray-700 dark:text-gray-300')"
    >
      {{ label }}
      <span v-if="required" class="text-red-500">*</span>
    </label>
    
    <div class="relative group">
      <div v-if="$slots.prefix || prefixIcon" class="absolute left-3 top-1/2 -translate-y-1/2 z-10 transition-all duration-200 group-focus-within:text-gray-700 dark:group-focus-within:text-gray-300" :class="error ? 'text-red-500 dark:text-red-400' : 'text-gray-400 dark:text-gray-500'">
        <slot name="prefix">
          <font-awesome-icon v-if="prefixIcon" :icon="prefixIcon" class="text-sm" />
        </slot>
      </div>
      
      <input
        :id="inputId"
        :type="type"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        :placeholder="placeholder"
        :disabled="disabled"
        :readonly="readonly"
        :required="required"
        :min="min"
        :max="max"
        :step="step"
        :autocomplete="autocomplete"
        class="relative w-full px-4 py-3 text-sm rounded-xl border-2 transition-all duration-200 focus:outline-none placeholder:text-gray-400 dark:placeholder:text-gray-500"
        :class="[
          inputClass,
          {
            'pl-10': $slots.prefix || prefixIcon,
            'pr-10': $slots.suffix || suffixIcon || error,
            'border-red-500 dark:border-red-400 focus:border-red-600 dark:focus:border-red-300 bg-red-50/50 dark:bg-red-950/20': error,
            'border-gray-200 dark:border-gray-700 focus:border-gray-900 dark:focus:border-white hover:border-gray-300 dark:hover:border-gray-600': !error && !disabled,
            'bg-white dark:bg-gray-900 text-gray-900 dark:text-gray-100': !disabled,
            'bg-gray-50 dark:bg-gray-900/50 text-gray-400 dark:text-gray-600 cursor-not-allowed border-gray-100 dark:border-gray-800': disabled,
            'bg-gray-50 dark:bg-gray-900/30': readonly
          }
        ]"
      />
      
      <div v-if="$slots.suffix || suffixIcon || error" class="absolute right-3 top-1/2 -translate-y-1/2 z-10 transition-all duration-200">
        <slot name="suffix">
          <font-awesome-icon 
            v-if="error" 
            icon="exclamation-circle" 
            class="text-sm text-red-500 dark:text-red-400" 
          />
          <font-awesome-icon 
            v-else-if="suffixIcon" 
            :icon="suffixIcon" 
            class="text-sm transition-colors duration-200 group-focus-within:text-gray-700 dark:group-focus-within:text-gray-300"
            :class="error ? 'text-red-500 dark:text-red-400' : 'text-gray-400 dark:text-gray-500'" 
          />
        </slot>
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
    type: [String, Number],
    default: ''
  },
  type: {
    type: String,
    default: 'text',
    validator: (value) => ['text', 'email', 'password', 'number', 'tel', 'url', 'search', 'date', 'time', 'datetime-local'].includes(value)
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
  prefixIcon: {
    type: String,
    default: ''
  },
  suffixIcon: {
    type: String,
    default: ''
  },
  inputClass: {
    type: String,
    default: ''
  },
  labelClass: {
    type: String,
    default: ''
  },
  min: {
    type: [String, Number],
    default: undefined
  },
  max: {
    type: [String, Number],
    default: undefined
  },
  step: {
    type: [String, Number],
    default: undefined
  },
  autocomplete: {
    type: String,
    default: 'off'
  }
})

defineEmits(['update:modelValue'])

const inputId = computed(() => `input-${Math.random().toString(36).substr(2, 9)}`)
</script>

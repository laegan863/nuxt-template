<script setup>
defineProps({
  // Card wrapper classes
  cardClass: {
    type: String,
    default: 'bg-white dark:bg-gray-800 rounded-3xl shadow-lg p-8 border border-gray-200 dark:border-gray-700'
  },
  // Card title
  title: {
    type: String,
    default: ''
  },
  // Title classes
  titleClass: {
    type: String,
    default: 'text-2xl font-bold text-gray-900 dark:text-white mb-6'
  },
  // Card subtitle
  subtitle: {
    type: String,
    default: ''
  },
  // Subtitle classes
  subtitleClass: {
    type: String,
    default: 'text-sm text-gray-500 dark:text-gray-400 mb-4'
  },
  // Show header divider
  divider: {
    type: Boolean,
    default: false
  },
  // Padding (can be overridden via cardClass)
  noPadding: {
    type: Boolean,
    default: false
  },
  // Shadow intensity
  shadow: {
    type: String,
    default: 'lg', // none, sm, md, lg, xl, 2xl
    validator: (value) => ['none', 'sm', 'md', 'lg', 'xl', '2xl'].includes(value)
  },
  // Border radius
  rounded: {
    type: String,
    default: '3xl', // none, sm, md, lg, xl, 2xl, 3xl, full
    validator: (value) => ['none', 'sm', 'md', 'lg', 'xl', '2xl', '3xl', 'full'].includes(value)
  }
})

const getShadowClass = (shadow) => {
  if (shadow === 'none') return 'shadow-none'
  return `shadow-${shadow}`
}

const getRoundedClass = (rounded) => {
  if (rounded === 'none') return 'rounded-none'
  return `rounded-${rounded}`
}
</script>

<template>
  <div 
    :class="[
      cardClass || [
        'bg-white dark:bg-gray-800',
        getRoundedClass(rounded),
        getShadowClass(shadow),
        noPadding ? '' : 'p-8',
        'border border-gray-200 dark:border-gray-700'
      ]
    ]"
  >
    <!-- Header Slot or Title/Subtitle -->
    <div v-if="$slots.header || title || subtitle" :class="divider ? 'pb-6 mb-6 border-b border-gray-200 dark:border-gray-700' : ''">
      <slot name="header">
        <h2 v-if="title" :class="titleClass">{{ title }}</h2>
        <p v-if="subtitle" :class="subtitleClass">{{ subtitle }}</p>
      </slot>
    </div>

    <!-- Default Content Slot -->
    <slot></slot>

    <!-- Footer Slot -->
    <div v-if="$slots.footer" :class="divider ? 'pt-6 mt-6 border-t border-gray-200 dark:border-gray-700' : 'mt-6'">
      <slot name="footer"></slot>
    </div>
  </div>
</template>

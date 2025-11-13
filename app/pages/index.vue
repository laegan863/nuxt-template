<template>
  <div></div>
</template>
<script setup>
useHead({
  title: 'Home - Admin Panel',
  meta: [
    { name: 'description', content: 'Welcome to the Admin Panel. Professional admin template built with Nuxt.js, Vue 3, and Tailwind CSS.' },
    { name: 'keywords', content: 'admin panel, dashboard, nuxt, vue, tailwind' },
    { property: 'og:title', content: 'Home - Admin Panel' },
    { property: 'og:description', content: 'Professional admin template built with Nuxt.js, Vue 3, and Tailwind CSS.' },
    { property: 'og:type', content: 'website' }
  ]
})

navigateTo('/dashboard')
</script>

<template>
  <NuxtLayout name="admin">
    <div>
      <!-- Breadcrumbs -->
      <Breadcrumbs :items="[{ label: 'Pages', to: '/dashboard' }, { label: 'Empty Page' }]" />
      
      <div class="flex items-center justify-center min-h-[calc(100vh-150px)]">
        <div class="text-center max-w-md px-6">
        <!-- Icon -->
        <div class="relative inline-block mb-8">
          <div class="w-32 h-32 mx-auto rounded-3xl bg-gradient-to-br from-gray-100 to-gray-200 dark:from-gray-800 dark:to-gray-700 flex items-center justify-center shadow-lg">
            <font-awesome-icon icon="file" class="text-5xl text-gray-400 dark:text-gray-500" />
          </div>
        </div>
        
        <!-- Content -->
        <h1 class="text-4xl font-bold text-gray-900 dark:text-white mb-4">
          Empty Page
        </h1>
        <p class="text-lg text-gray-600 dark:text-gray-400 mb-8 leading-relaxed">
          This is an empty page template. Start building something amazing here!
        </p>
        
        <!-- Actions -->
        <div class="flex flex-col sm:flex-row gap-4 justify-center">
          <NuxtLink 
            to="/dashboard" 
            class="inline-flex items-center justify-center gap-3 px-6 py-3 rounded-xl bg-gray-900 dark:bg-gray-700 hover:bg-gray-800 dark:hover:bg-gray-600 text-white font-medium shadow-md hover:shadow-lg hover:-translate-y-0.5 transition-all duration-300"
          >
            <font-awesome-icon icon="home" />
            <span>Go to Dashboard</span>
          </NuxtLink>
          
          <button class="inline-flex items-center justify-center gap-3 px-6 py-3 rounded-xl bg-white dark:bg-gray-800 hover:bg-gray-50 dark:hover:bg-gray-700 text-gray-700 dark:text-gray-200 font-medium border-2 border-gray-200 dark:border-gray-700 hover:border-gray-300 dark:hover:border-gray-600 shadow-md hover:shadow-lg hover:-translate-y-0.5 transition-all duration-300">
            <font-awesome-icon icon="plus" />
            <span>Add Content</span>
          </button>
        </div>
        
        <!-- Decorative elements -->
        <div class="mt-12 flex items-center justify-center gap-2">
          <div class="w-2 h-2 rounded-full bg-gray-400 dark:bg-gray-600 animate-pulse"></div>
          <div class="w-2 h-2 rounded-full bg-gray-400 dark:bg-gray-600 animate-pulse delay-100"></div>
          <div class="w-2 h-2 rounded-full bg-gray-400 dark:bg-gray-600 animate-pulse delay-200"></div>
        </div>
      </div>
      </div>
    </div>
  </NuxtLayout>
</template>

<script setup>
definePageMeta({
  layout: false
})

useHead({
  title: 'Empty Page - Admin Panel',
  meta: [
    { name: 'description', content: 'Empty page template ready for your custom content. Start building something amazing here!' },
    { name: 'keywords', content: 'empty page, template, blank page' },
    { property: 'og:title', content: 'Empty Page - Admin Panel' },
    { property: 'og:description', content: 'Empty page template ready for your custom content.' },
    { property: 'og:type', content: 'website' }
  ]
})
</script>

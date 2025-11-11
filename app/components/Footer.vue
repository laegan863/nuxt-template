<template>
  <footer class="mt-auto border-t border-gray-200 dark:border-gray-700 bg-white dark:bg-gray-800 py-6">
    <div class="px-6">
      <div class="flex flex-col md:flex-row justify-between items-center gap-4">
        <!-- Copyright -->
        <div class="text-sm text-gray-600 dark:text-gray-400">
          © {{ currentYear }} <span class="font-semibold text-gray-900 dark:text-white">Admin Panel</span>. All rights reserved.
        </div>
        
        <!-- Links -->
        <div class="flex items-center gap-6">
          <a href="#" class="text-sm text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors">
            Privacy Policy
          </a>
          <a href="#" class="text-sm text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors">
            Terms of Service
          </a>
          <a href="#" class="text-sm text-gray-600 dark:text-gray-400 hover:text-gray-900 dark:hover:text-white transition-colors">
            Support
          </a>
        </div>
        
        <!-- Version -->
        <div class="text-sm text-gray-500 dark:text-gray-500">
          v1.0.0
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
const currentYear = new Date().getFullYear()
</script>

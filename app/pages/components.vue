
<script setup>
import { ref } from 'vue'

definePageMeta({
  layout: false
})

useHead({
  title: 'UI Components - Admin Panel',
  meta: [
    { name: 'description', content: 'Advanced UI components including data tables, modals, and alerts for building professional interfaces. Fully customizable with dark mode support.' },
    { name: 'keywords', content: 'ui components, data tables, modals, alerts, notifications' },
    { property: 'og:title', content: 'UI Components - Admin Panel' },
    { property: 'og:description', content: 'Advanced UI components for building professional interfaces.' },
    { property: 'og:type', content: 'website' }
  ]
})

const alerts = ref({
  info: true,
  success: true,
  warning: true,
  error: true,
  custom: true
})

const resetAlerts = () => {
  alerts.value = {
    info: true,
    success: true,
    warning: true,
    error: true,
    custom: true
  }
}

const modals = ref({
  small: false,
  medium: false,
  large: false,
  withFooter: false,
  confirmation: false,
})

const modalFormData = ref({
  name: '',
  email: ''
})

const handleModalSave = () => {
  console.log('Saving changes...')
  modals.value.withFooter = false
  alerts.value.success = true
}

const handleDelete = () => {
  console.log('Deleting item...')
  modals.value.confirmation = false
  alerts.value.success = true
}

</script>
<template>
  <NuxtLayout name="admin">
    <div class="space-y-8">
      <!-- Breadcrumbs -->
      <Breadcrumbs :items="[{ label: 'Pages', link: '#' }, { label: 'UI Components' }]" />
      
      <!-- Header -->
      <div class="relative overflow-hidden">
        <div class="absolute -top-20 -left-20 w-72 h-72 bg-indigo-400/10 dark:bg-indigo-500/5 rounded-full blur-3xl"></div>
        <div class="absolute -top-20 -right-20 w-72 h-72 bg-purple-400/10 dark:bg-purple-500/5 rounded-full blur-3xl"></div>
        <div class="relative">
          <div class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-gradient-to-r from-indigo-50 to-purple-50 dark:from-indigo-900/30 dark:to-purple-900/30 border border-indigo-200 dark:border-indigo-800 mb-4">
            <font-awesome-icon icon="cubes" class="text-indigo-600 dark:text-indigo-400 text-sm" />
            <span class="text-sm font-semibold bg-gradient-to-r from-indigo-600 to-purple-600 dark:from-indigo-400 dark:to-purple-400 bg-clip-text text-transparent">Advanced Components</span>
          </div>
          <h1 class="text-5xl font-black bg-gradient-to-r from-gray-900 via-gray-800 to-gray-600 dark:from-white dark:via-gray-200 dark:to-gray-400 bg-clip-text text-transparent mb-4 leading-tight">
            UI Components
          </h1>
          <p class="text-lg text-gray-600 dark:text-gray-400 max-w-3xl leading-relaxed">
            Data tables, modals, and alerts for building professional interfaces
          </p>
        </div>
      </div>

      <div class="space-y-6">
        <!-- Alerts Section -->
        <BaseCard>
          <template #header>
            <div class="flex items-center gap-4">
              <div class="relative">
                <div class="absolute inset-0 bg-gradient-to-r from-blue-500 to-cyan-600 rounded-2xl blur-md opacity-50"></div>
                <div class="relative w-14 h-14 rounded-2xl bg-gradient-to-br from-blue-500 to-cyan-600 flex items-center justify-center shadow-xl">
                  <font-awesome-icon icon="bell" class="text-white text-xl" />
                </div>
              </div>
              <div>
                <h2 class="text-2xl font-bold text-gray-900 dark:text-white">Alerts</h2>
                <p class="text-sm text-gray-500 dark:text-gray-400">Notification messages with different types</p>
              </div>
            </div>
          </template>

          <div class="space-y-4">
            <BaseAlert
              v-model="alerts.info"
              type="info"
              title="Information"
              message="This is an informational alert message with useful details."
            />

            <BaseAlert
              v-model="alerts.success"
              type="success"
              title="Success!"
              message="Your action was completed successfully."
            />

            <BaseAlert
              v-model="alerts.warning"
              type="warning"
              title="Warning"
              message="Please review this warning before proceeding."
            />

            <BaseAlert
              v-model="alerts.error"
              type="error"
              title="Error"
              message="An error occurred. Please try again later."
            />

            <BaseAlert
              v-model="alerts.custom"
              type="info"
              title="Custom Content"
            >
              <p class="mb-2">You can use custom content in alerts with:</p>
              <ul class="list-disc list-inside space-y-1">
                <li>Bullet points</li>
                <li>Links and <strong>formatted text</strong></li>
                <li>Any custom HTML content</li>
              </ul>
            </BaseAlert>

            <div class="flex gap-2 pt-2">
              <BaseButton 
                size="sm" 
                variant="outline" 
                label="Reset Alerts"
                @click="resetAlerts"
              />
            </div>
          </div>
        </BaseCard>

      </div>
    </div>
  </NuxtLayout>
</template>


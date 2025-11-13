
<script setup>
import { ref } from 'vue'

definePageMeta({
  layout: false
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
        <div class="bg-white dark:bg-gray-800 rounded-3xl shadow-lg p-8 border border-gray-200 dark:border-gray-700">
          <div class="flex items-center gap-4 mb-6">
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
        </div>

        <!-- Modals Section -->
        <div class="bg-white dark:bg-gray-800 rounded-3xl shadow-lg p-8 border border-gray-200 dark:border-gray-700">
          <div class="flex items-center gap-4 mb-6">
            <div class="relative">
              <div class="absolute inset-0 bg-gradient-to-r from-purple-500 to-pink-600 rounded-2xl blur-md opacity-50"></div>
              <div class="relative w-14 h-14 rounded-2xl bg-gradient-to-br from-purple-500 to-pink-600 flex items-center justify-center shadow-xl">
                <font-awesome-icon icon="window-restore" class="text-white text-xl" />
              </div>
            </div>
            <div>
              <h2 class="text-2xl font-bold text-gray-900 dark:text-white">Modals</h2>
              <p class="text-sm text-gray-500 dark:text-gray-400">Dialog boxes with different sizes</p>
            </div>
          </div>

          <div class="flex flex-wrap gap-3">
            <BaseButton 
              variant="primary" 
              label="Small Modal" 
              @click="modals.small = true"
            />
            <BaseButton 
              variant="secondary" 
              label="Medium Modal" 
              @click="modals.medium = true"
            />
            <BaseButton 
              variant="success" 
              label="Large Modal" 
              @click="modals.large = true"
            />
            <BaseButton 
              variant="info" 
              label="With Footer" 
              @click="modals.withFooter = true"
            />
            <BaseButton 
              variant="warning" 
              label="Confirmation" 
              @click="modals.confirmation = true"
            />
          </div>

          <!-- Modal Components -->
          <BaseModal
            v-model="modals.small"
            size="sm"
            title="Small Modal"
            subtitle="This is a small sized modal"
          >
            <p class="text-gray-600 dark:text-gray-400">
              This is a small modal dialog. Perfect for simple messages or confirmations.
            </p>
          </BaseModal>

          <BaseModal
            v-model="modals.medium"
            size="md"
            title="Medium Modal"
            subtitle="This is a medium sized modal"
          >
            <p class="text-gray-600 dark:text-gray-400 mb-4">
              This is a medium modal dialog with more content space.
            </p>
            <div class="space-y-3">
              <BaseInput
                v-model="modalFormData.name"
                label="Name"
                placeholder="Enter your name"
              />
              <BaseInput
                v-model="modalFormData.email"
                type="email"
                label="Email"
                placeholder="you@example.com"
              />
            </div>
          </BaseModal>

          <BaseModal
            v-model="modals.large"
            size="lg"
            title="Large Modal"
            subtitle="This is a large sized modal with more content"
          >
            <p class="text-gray-600 dark:text-gray-400 mb-4">
              This is a large modal dialog suitable for forms and detailed content.
            </p>
            <div class="grid grid-cols-2 gap-4">
              <BaseInput label="First Name" placeholder="John" />
              <BaseInput label="Last Name" placeholder="Doe" />
              <BaseInput label="Email" type="email" placeholder="john@example.com" />
              <BaseInput label="Phone" type="tel" placeholder="+1 234 567 8900" />
              <div class="col-span-2">
                <BaseTextarea label="Message" placeholder="Your message..." :rows="4" />
              </div>
            </div>
          </BaseModal>

          <BaseModal
            v-model="modals.withFooter"
            title="Modal with Footer"
            subtitle="Custom footer with action buttons"
          >
            <template #default>
              <p class="text-gray-600 dark:text-gray-400">
                This modal includes a footer with custom action buttons.
              </p>
            </template>
            <template #footer>
              <BaseButton variant="ghost" label="Cancel" @click="modals.withFooter = false" />
              <BaseButton variant="primary" label="Save Changes" @click="handleModalSave" />
            </template>
          </BaseModal>

          <BaseModal
            v-model="modals.confirmation"
            size="sm"
            title="Delete Item?"
            subtitle="This action cannot be undone"
          >
            <template #default>
              <p class="text-gray-600 dark:text-gray-400">
                Are you sure you want to delete this item? This action is permanent and cannot be reversed.
              </p>
            </template>
            <template #footer>
              <BaseButton variant="ghost" label="Cancel" @click="modals.confirmation = false" />
              <BaseButton variant="danger" label="Delete" prefix-icon="trash" @click="handleDelete" />
            </template>
          </BaseModal>
        </div>
      </div>
    </div>
  </NuxtLayout>
</template>


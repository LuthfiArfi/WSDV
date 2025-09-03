<template>
  <Transition name="fade-scale">
    <div v-if="isOpen" class="fixed inset-0 z-50 flex items-center justify-center bg-black bg-opacity-50">
      <Transition name="fade-scale-inner">
        <div class="bg-white rounded-lg shadow-lg max-w-md w-full p-6">
          <h2 class="text-xl font-semibold mb-4">{{ title }}</h2>
          <p class="mb-6">{{ message }}</p>
          <div class="flex justify-end space-x-2">
            <button @click="close" class="px-4 py-2 bg-gray-300 rounded hover:bg-gray-400">Cancel</button>
            <button @click="confirm" class="px-4 py-2 bg-blue-600 text-white rounded hover:bg-blue-700">OK</button>
          </div>
        </div>
      </Transition>
    </div>
  </Transition>
</template>

<script setup>
defineProps({
  isOpen: Boolean,
  title: String,
  message: String
})

const emit = defineEmits(['close', 'confirm'])

const close = () => emit('close')
const confirm = () => emit('confirm')
</script>

<style scoped>
.fade-scale-enter-active,
.fade-scale-leave-active {
  transition: opacity 0.3s ease;
}
.fade-scale-enter-from,
.fade-scale-leave-to {
  opacity: 0;
}

.fade-scale-inner-enter-active,
.fade-scale-inner-leave-active {
  transition: transform 0.3s ease, opacity 0.3s ease;
}
.fade-scale-inner-enter-from,
.fade-scale-inner-leave-to {
  transform: scale(0.95);
  opacity: 0;
}
</style>

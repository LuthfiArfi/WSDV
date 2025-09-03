<template>
  <Transition name="fade-scale">
    <div v-if="isOpen" class="fixed inset-0 z-50 flex items-center justify-center bg-black/50">
      <Transition name="fade-scale-inner">
        <div class="bg-white rounded-lg shadow-lg max-w-md w-full p-6">
          <h2 class="text-xl text-center font-semibold mb-4">{{ title }}</h2>
          <p class="mb-2 text-center">{{ message }}</p>
          <p class="text-sm text-gray-500">Menutup dalam {{ remainingTime }} detik...</p>
          <div class="flex justify-center mt-4">
            <button
            @click="emit('close')"
            class="px-4 py-1 bg-sky-600 text-white rounded item-center text-sm"
            >
            Tutup
            </button>
        </div>
        </div>
      </Transition>
    </div>
  </Transition>
</template>

<script setup>
import { watch, ref, onUnmounted } from 'vue'

const props = defineProps({
  isOpen: Boolean,
  title: String,
  message: String,
  duration: {
    type: Number,
    default: 3000 // dalam milidetik
  }
})

const emit = defineEmits(['close'])

const remainingTime = ref(0)
let intervalId
let timeoutId

const startCountdown = () => {
  remainingTime.value = Math.ceil(props.duration / 1000)

  // Set interval untuk update setiap detik
  intervalId = setInterval(() => {
    remainingTime.value -= 1
  }, 1000)

  // Set timeout untuk menutup modal
  timeoutId = setTimeout(() => {
    emit('close')
  }, props.duration)
}

const stopCountdown = () => {
  clearInterval(intervalId)
  clearTimeout(timeoutId)
}

watch(() => props.isOpen, (val) => {
  if (val) {
    startCountdown()
  } else {
    stopCountdown()
  }
})

onUnmounted(() => {
  stopCountdown()
})
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
  transform: scale(0.75);
  opacity: 0;
}
</style>

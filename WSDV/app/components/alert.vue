<template>
  <div
    v-if="show"
    :class="[
      'flex items-center p-4 rounded-md shadow',
      typeClasses,
      'text-white',
      'space-x-3',
      'transition-opacity duration-300',
      show ? 'opacity-100' : 'opacity-0'
    ]"
    role="alert"
  >
    <slot name="icon">
      <!-- Default icons for each type -->
      <template v-if="type === 'success'">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" d="M5 13l4 4L19 7" />
        </svg>
      </template>
      <template v-else-if="type === 'error'">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
        </svg>
      </template>
      <template v-else-if="type === 'warning'">
        <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" d="M12 9v2m0 4h.01M4.93 19h14.14a1 1 0 0 0 .86-1.49L13.86 5a1 1 0 0 0-1.72 0L4.07 17.5A1 1 0 0 0 4.93 19z"/>
        </svg>
      </template>
      <template v-else>
        <!-- info / default -->
        <svg class="w-6 h-6" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
          <path stroke-linecap="round" stroke-linejoin="round" d="M13 16h-1v-4h-1m1-4h.01M12 12v.01" />
        </svg>
      </template>
    </slot>

    <div class="flex-1">
      <slot />
    </div>

    <button
    v-if="dismissible"
    @click="close"
    class="flex items-center justify-center w-6 h-6 rounded-md bg-white bg-opacity-20 hover:bg-opacity-80 text-black hover:text-gray-700 focus:outline-none transition"
    aria-label="Close"
    >
    <svg class="w-4 h-4" fill="none" stroke="currentColor" stroke-width="2" viewBox="0 0 24 24">
        <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
    </svg>
    </button>
  </div>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
  type: {
    type: String,
    default: 'info', // success, error, warning, info
    validator: val => ['success', 'error', 'warning', 'info'].includes(val)
  },
  dismissible: {
    type: Boolean,
    default: false
  },
  modelValue: {
    type: Boolean,
    default: false
  }
})

const emit = defineEmits(['update:modelValue', 'dismissed'])

const show = computed({
  get: () => props.modelValue,
  set: (val) => emit('update:modelValue', val)
})


watch(() => props.modelValue, (newVal) => {
  show.value = newVal
})

const close = () => {
  show.value = false
  emit('update:modelValue', false)
  emit('dismissed')
}

const typeClasses = {
  success: 'bg-green-600',
  error: 'bg-red-600',
  warning: 'bg-yellow-500',
  info: 'bg-blue-600'
}[props.type]
</script>

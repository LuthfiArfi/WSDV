<template>
    <div class="flex items-center space-x-4">
      <input
        type="color"
        v-model="selectedColor"
        @input="emitColor"
        class="w-10 h-10 border rounded"
      />
      <span class="text-sm">Warna Terpilih:</span>
      <div
        class="w-10 h-10 border rounded"
        :style="{ backgroundColor: selectedColor }"
      ></div>
      <span class="text-xs font-mono">{{ selectedColor }}</span>
    </div>
  </template>
  
  <script setup>
  import { ref, watch } from 'vue'
  
  const props = defineProps({
    modelValue: {
      type: String,
      default: '#ff0000'
    }
  })
  
  const emit = defineEmits(['update:modelValue'])
  
  const selectedColor = ref(props.modelValue)
  
  // Watcher untuk update prop ke emit
  watch(selectedColor, (val) => {
    emit('update:modelValue', val)
  })
  
  // Emit saat pengguna memilih warna
  function emitColor(event) {
    selectedColor.value = event.target.value
  }
  </script>
  
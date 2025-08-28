<template>
    <div class="flex flex-col space-y-1">
      <label :for="id" class="text-sm font-medium">{{ label }}</label>
      <input
        :id="id"
        type="date"
        :value="modelValue"
        @input="$emit('update:modelValue', $event.target.value)"
        class="border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white text-gray-800"
      />
    </div>
  </template>
  
  <script setup>
  const props = defineProps({
    modelValue: String,
    label: {
      type: String,
      default: 'Tanggal'
    },
    id: {
      type: String,
      default: 'date-picker'
    }
  })
  
  defineEmits(['update:modelValue'])
  </script>
  
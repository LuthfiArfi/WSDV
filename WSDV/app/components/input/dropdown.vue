<template>
    <div class="flex flex-col space-y-1">
      <label :for="id" class="text-sm font-medium text-gray-700">{{ label }}</label>
      <select
        :id="id"
        :value="modelValue"
        @change="$emit('update:modelValue', $event.target.value)"
        class="border border-gray-300 rounded px-3 py-2 focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 bg-white text-gray-800"
      >
        <option disabled value="">-- Pilih opsi --</option>
        <option v-for="(option, index) in options" :key="index" :value="option.value">
          {{ option.label }}
        </option>
      </select>
    </div>
  </template>
  
  <script setup>
  const props = defineProps({
    modelValue: String,
    label: {
      type: String,
      default: 'Pilih Opsi'
    },
    id: {
      type: String,
      default: 'dropdown-list'
    },
    options: {
      type: Array,
      default: () => []
    }
  })
  
  defineEmits(['update:modelValue'])
  </script>
  
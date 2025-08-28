<template>
  <div>
    <label :for="label" class="text-sm font-medium">{{ label }}</label>
    <input
      :id="label"
      :type="type"
      :placeholder="placeholder"
      :class="inputClass"
      :value="modelValue"
      :disabled="disabled"
      @input="$emit('update:modelValue', $event.target.value)"
      class="border border-gray-300 rounded px-3 py-2 bg-white text-gray-900 
      focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 
      disabled:border-gray-200 disabled:bg-gray-200 disabled:text-gray-500 disabled:shadow-none "
    />
  </div>
</template>

<script setup>
defineProps({
  label: String,
  modelValue: [String, Number],
  type: {
    type: String,
    default: 'text'
  },
  placeholder: {
    type: String,
    default: ''
  },
  inputClass: {
    type: String,
    default: 'input'
  },
  disabled: {
    type: Boolean,
    default: false
  }
})

defineEmits(['update:modelValue'])
</script>

<style scoped>
input {
  display: block;
  width: 100%;
  padding: 0.5rem;
  margin-top: 0.25rem;
  border: 1px solid #ccc;
  border-radius: 0.375rem;
  
}
</style>

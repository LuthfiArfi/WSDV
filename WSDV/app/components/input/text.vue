<template>
  <div>
    <label :for="label" class="block mb-1 font-medium">{{ label }}</label>
    <input
      :id="label"
      :type="type"
      :placeholder="placeholder"
      :class="inputClass"
      :value="modelValue"
      @input="$emit('update:modelValue', $event.target.value)"
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
  background-color: #ffffff;
}
</style>
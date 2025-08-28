<template>
  <div>
    <label class="text-sm font-medium mb-2">Daftar Attendees</label>
    <div v-for="(attendee, index) in modelValue" :key="index" class="flex gap-2 mb-2">
      <input
        :value="attendee"
        @input="updateAttendee(index, $event.target.value)"
        class="flex-1 border border-gray-300 rounded px-3 py-2 bg-white text-gray-900 
      focus:outline-none focus:ring-2 focus:ring-blue-500 focus:border-blue-500 "
        placeholder="Nama Attendee"
      />
      <button @click="removeAttendee(index)" class="text-red-500">✕</button>
    </div>
    <button @click="addAttendee" class="bg-sky-500 text-white px-3 py-1 rounded item-center">+ Add</button>
  </div>
</template>

<script setup>
import { onMounted } from 'vue'

const props = defineProps({
  modelValue: {
    type: Array,
    default: () => []
  }
})

const emit = defineEmits(['update:modelValue'])

const addAttendee = () => {
  emit('update:modelValue', [...props.modelValue, ''])
}

const removeAttendee = (index) => {
  const updated = [...props.modelValue]
  updated.splice(index, 1)
  emit('update:modelValue', updated)
}

const updateAttendee = (index, value) => {
  const updated = [...props.modelValue]
  updated[index] = value
  emit('update:modelValue', updated)
}

// ⬇️ Tambahkan satu attendee jika kosong saat mount
onMounted(() => {
  if (!props.modelValue || props.modelValue.length === 0) {
    emit('update:modelValue', [''])
  }
})
</script>

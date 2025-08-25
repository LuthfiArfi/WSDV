<template>
      <button
        :type="type"
        :class="[
          'px-4 py-2 rounded-md font-medium transition duration-200 ease-in-out',
          variant === 'primary' ? 'bg-blue-600 text-white hover:bg-blue-700' : '',
          variant === 'secondary' ? 'bg-gray-200 text-gray-800 hover:bg-gray-300' : '',
          variant === 'danger' ? 'bg-red-600 text-white hover:bg-red-700' : '',
          disabled ? 'opacity-50 cursor-not-allowed' : ''
        ]"
        :disabled="disabled"
        @click="handleClick"
        >
        <slot>{{ label }}</slot>
      </button>
</template>

<script setup>
const props = defineProps({
  label: {
    type: String,
    default: 'Klik Saya'
  },
  type: {
    type: String,
    default: 'button'
  },
  variant: {
    type: String,
    default: 'primary'
  },
  disabled: {
    type: Boolean,
    default: false
  },
  onClick: Function
})

const handleClick = () => {
  if (!props.disabled && typeof props.onClick === 'function') {
    props.onClick()
  }
}
</script>

<template>
  <div class="overflow-x-auto">
    <table class="table-auto w-full border-y border-black">
      <thead class="bg-rose-200">
        <tr>
          <th
            v-for="col in columns"
            :key="col.key"
            class="p-2 text-xl border-y border-black cursor-pointer select-none"
            @click="sortBy(col.key)"
          >
            {{ col.label }}
            <span v-if="sortColumn === col.key">
              {{ sortAsc ? '↑' : '↓' }}
            </span>
          </th>
        </tr>
      </thead>
      <tbody>
        <tr
          v-for="(row, rowIndex) in sortedData"
          :key="rowIndex"
          class="hover:bg-slate-200"
        >
          <td
            v-for="col in columns"
            :key="col.key"
            class="p-2 text-center"
          >
            {{ row[col.key] }}
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script setup>
import { ref, computed } from 'vue'

const props = defineProps({
  data: {
    type: Array,
    required: true,
  },
  columns: {
    type: Array,
    required: true,
  },
})

const sortColumn = ref(null)
const sortAsc = ref(true)

function sortBy(key) {
  if (sortColumn.value === key) {
    sortAsc.value = !sortAsc.value
  } else {
    sortColumn.value = key
    sortAsc.value = true
  }
}

const sortedData = computed(() => {
  if (!sortColumn.value) return props.data
  return [...props.data].sort((a, b) => {
    const valA = a[sortColumn.value]
    const valB = b[sortColumn.value]

    if (typeof valA === 'number' && typeof valB === 'number') {
      return sortAsc.value ? valA - valB : valB - valA
    }

    return sortAsc.value
      ? String(valA).localeCompare(String(valB))
      : String(valB).localeCompare(String(valA))
  })
})
</script>

<style scoped>
table {
  border-collapse: collapse;
}
</style>

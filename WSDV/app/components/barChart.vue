<script setup>
import { ref, watch, onMounted } from 'vue'
import {
  Chart,
  BarController,
  BarElement,
  CategoryScale,
  LinearScale,
  Tooltip,
  Legend
} from 'chart.js'

// ✅ Registrasi lengkap untuk chart tipe "bar"
Chart.register(BarController, BarElement, CategoryScale, LinearScale, Tooltip, Legend)

const props = defineProps({
  title: { type: String, default: 'Bar Chart' },
  modelValue: {
    type: Object,
    required: true,
    validator: (val) =>
      Array.isArray(val.labels) &&
      Array.isArray(val.dataset?.data) &&
      typeof val.dataset?.label === 'string'
  }
})

const emit = defineEmits(['update:modelValue'])

const canvas = ref(null)
let chartInstance = null

const renderChart = () => {
  if (chartInstance) chartInstance.destroy()

  chartInstance = new Chart(canvas.value, {
    type: 'bar',
    data: {
      labels: props.modelValue.labels,
      datasets: [{
        label: props.modelValue.dataset.label,
        data: props.modelValue.dataset.data,
        backgroundColor: '#3b82f6',
        borderRadius: 4
      }]
    },
    options: {
      responsive: true,
      plugins: {
        legend: { display: true },
        tooltip: { enabled: true }
      },
      scales: {
        y: { beginAtZero: true }
      }
    }
  })
}

onMounted(renderChart)
watch(() => props.modelValue, renderChart, { deep: true })
</script>

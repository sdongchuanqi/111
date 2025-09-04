<template>
  <div style="margin-top: 20px">
    <v-chart :option="chartOptions" autoresize style="height:400px" />
  </div>
</template>

<script setup>
import { computed } from 'vue'
import { use } from 'echarts/core'
import { CanvasRenderer } from 'echarts/renderers'
import { BarChart } from 'echarts/charts'
import {
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent
} from 'echarts/components'
import VChart from 'vue-echarts'

use([CanvasRenderer, BarChart, TitleComponent, TooltipComponent, GridComponent, LegendComponent])

const props = defineProps({
  data: { type: Array, required: true }
})

const chartOptions = computed(() => {
  const grouped = props.data.reduce((acc, item) => {
    acc[item.project] = (acc[item.project] || 0) + item.hours
    return acc
  }, {})

  return {
    title: { text: 'Project Hours Distribution', left: 'center' },
    tooltip: {},
    xAxis: { type: 'category', data: Object.keys(grouped) },
    yAxis: { type: 'value' },
    series: [
      {
        name: 'Hours',
        type: 'bar',
        data: Object.values(grouped)
      }
    ]
  }
})
</script>

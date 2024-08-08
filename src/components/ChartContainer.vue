<template>
  <v-chart :option="option" autoresize/>
</template>

<script setup lang="ts">

import { use } from 'echarts/core'
import { BarChart, ScatterChart, PieChart, LineChart } from 'echarts/charts'
import { CanvasRenderer } from 'echarts/renderers'
import { 
  TitleComponent,
  GridComponent,
  TooltipComponent,
  LegendComponent } from 'echarts/components'


const props = defineProps<{
  title?: string
  chartType?: string
  option?: object
  data?: object
}>()

use([
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent,
  CanvasRenderer
])

switch (props.chartType) {
  case 'bar': 
    use([BarChart])
    break
  case 'scatter':
    use([ScatterChart])
    break
  case 'pie':
    use([PieChart])
    break
  case 'line':
    use([LineChart])
    break 
  default:
    console.log("Chart type not supported!")
    break
}





</script>

<style scoped>
v-chart {
  height: inherit;
  width: inherit;
}
</style>
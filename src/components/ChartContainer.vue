<template>
  <v-chart :option="option" autoresize/>
</template>

<script setup lang="ts">
import { ref } from 'vue'

import { use } from 'echarts/core'
import { BarChart, ScatterChart, PieChart, LineChart } from 'echarts/charts'
import {
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent
} from 'echarts/components'
import { CanvasRenderer } from 'echarts/renderers'
import type { ComposeOption } from 'echarts/core'
import type { BarSeriesOption } from 'echarts'
import type {
  TitleComponentOption,
  TooltipComponentOption,
  GridComponentOption,
  LegendComponentOption
} from 'echarts/components'



const props = defineProps<{
  titleText?: string
  chartType?: string
  // option?: object
  data?: object
}>()

use([
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent,
  CanvasRenderer
])

// type EChartComponentOptions = TitleComponentOption | TooltipComponentOption | GridComponentOption | LegendComponentOption
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

type EChartsOption = ComposeOption<
  | TitleComponentOption
  | TooltipComponentOption
  | GridComponentOption
  | LegendComponentOption
  | BarSeriesOption
>

let option: EChartsOption = {
  textStyle: {
    fontFamily: 'Inter, "Helvetica Neue"'
  },
  title: {
    text: props.titleText,
    left: 'center',
  }, 
  tooltip: {
    trigger: 'item',
    formatter: '{a} <br/> {b} : {c}'
  },
  xAxis: {
    type: 'category',
    data: ['MON', 'TUE', 'WED', 'THR', 'FRI', 'SAT', 'SUN']
  },
  yAxis: {
    type: 'value',
  },
  legend: {
    data: ['Sales'],
    right: 10,
  },
  series: {
    name: 'Sales',
    data: ['30000', '40000', '50000', '10000', '5000', '7900', '4500'],
    type: 'bar'
  }
}




</script>

<style scoped>
v-chart {
  height: inherit;
  width: inherit;
}
</style>
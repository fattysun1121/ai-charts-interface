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

let option = ref({})
type EChartsBaseOption = TitleComponentOption | TooltipComponentOption | GridComponentOption | LegendComponentOption
switch (props.chartType) {
  case 'bar':
    interface BarData {
      category: Array<string>;
      series: Array<BarSeriesOption>;
    }
    use([BarChart])
    type BarOption = ComposeOption<EChartsBaseOption | BarSeriesOption>
    const barData: BarData = props.data as BarData
    const barOption: BarOption= {
      // textStyle: {
      //   fontFamily: 'Inter, "Helvetica Neue"'
      // },
      title: {
        text: props.titleText,
        left: 'center',
      }, 
        // tooltip: {
        //   trigger: 'item',
        //   formatter: '{a} <br/> {b} : {c}'
        // },
      xAxis: {
        type: 'category',
        data: barData.category
      },
      yAxis: {
        type: 'value',
      },
      legend: {
        data: barData.series.map(element => (element.name as string)),
        right: 10,
      },
      series: barData.series 
    }
    option.value = barOption
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
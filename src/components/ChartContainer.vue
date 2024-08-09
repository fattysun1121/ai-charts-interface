<template>
  <select v-model="selected">
    <option disabled value="">Please select one</option>
    <option value="dark">Dark</option>
    <option value="infographic">infographic</option>
  </select>
  
  <v-chart :option="option" autoresize/>
</template>

<script setup lang="ts">
import { ref } from 'vue'

import { use, registerTheme } from 'echarts/core'
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

import { THEME_KEY } from 'vue-echarts'
import { provide } from 'vue'
import infographic from '../themes/infographic.json'

const selected = ref('')
registerTheme('infographic', infographic)
// composition API
// provide(THEME_KEY, selected)


const props = defineProps<{
  titleText?: string
  chartType?: string
  data?: object
}>()

use([
  BarChart,
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent,
  CanvasRenderer
])

let option = ref({
  "textStyle": {
    "fontFamily": "Inter, 'Helvetica Neue'"
  },
  "title": {
    "text": "Weekly Sales",
    "left": "center"
  }, 

  "tooltip": {
    "trigger": "item",
    "formatter": "{a} <br/> {b} : {c}"
  },
  "xAxis": {
    "type": "category",
    "data": ["MON", "TUE", "WED", "THR", "FRI", "SAT", "SUN"]
  },
  "yAxis": {
    "type": "value"
  },
  "legend": {
    "data": ["Sales"],
    "right": 10
  },
  "series": {
    "name": "Sales",
    "data": ["30000", "40000", "50000", "10000", "5000", "7900", "4500"],
    "type": "bar",
    "showBackGround": true,
    "backgroundStyle": {
      "color": "rgba(180, 180, 180, 0.2)"
    }
  }
}
)


// type EChartsBaseOption = TitleComponentOption | TooltipComponentOption | GridComponentOption | LegendComponentOption
// switch (props.chartType) {
//   case 'bar':
//     interface BarData {
//       category: Array<string>;
//       series: Array<BarSeriesOption>;
//     }
//     use([BarChart])
//     type BarOption = ComposeOption<EChartsBaseOption | BarSeriesOption>
//     const barData: BarData = props.data as BarData
//     const barOption: BarOption= {
//       title: {
//         text: props.titleText,
//         left: 'center',
//       }, 
//       xAxis: {
//         type: 'category',
//         data: barData.category
//       },
//       yAxis: {
//         type: 'value',
//       },
//       legend: {
//         data: barData.series.map(element => (element.name as string)),
//         right: 10,
//       },
//       series: barData.series 
//     }
//     option.value = barOption
//     break
//   case 'scatter':
//     use([ScatterChart])
//     break
//   case 'pie':
//     use([PieChart])
//     break
//   case 'line':
//     use([LineChart])
//     break 
//   default:
//     console.log("Chart type not supported!")
//     break
// }

</script>

<style scoped>
v-chart {
  height: 100%;
  width: 100%;
}
</style>
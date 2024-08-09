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
import type { 
  BarSeriesOption,
  ScatterSeriesOption, 
  PieSeriesOption, 
  LineSeriesOption 
} from 'echarts'
import type {
  TitleComponentOption,
  TooltipComponentOption,
  GridComponentOption,
  LegendComponentOption,

} from 'echarts/components'


// 主題相關
import { THEME_KEY } from 'vue-echarts'
import { provide } from 'vue'
import infographic from '../themes/infographic.json'

const selected = ref('')
registerTheme('infographic', infographic)
// composition API
provide(THEME_KEY, selected)


const props = defineProps<{
  titleText?: string
  chartType?: string
  data?: object
}>()

// 指定要使用的組件
use([
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent,
  CanvasRenderer
])


const option = ref({})

type EChartsBaseOption = TitleComponentOption | TooltipComponentOption | GridComponentOption | LegendComponentOption

// 決定要渲染的圖形，以及製作要提供渲染模組的option
switch (props.chartType) {
  case 'bar':
    use([BarChart])
    interface BarData {
      titleText: string;
      category: Array<string>;
      yName: string;
      xName: string; 
      series: Array<BarSeriesOption>;
    }
    type BarOption = ComposeOption<EChartsBaseOption | BarSeriesOption>
    const barData: BarData = props.data as BarData
    const barOption: BarOption = {
      title: {
        text: barData.titleText,
        left: 'center',
      },
      xAxis: {
        type: 'category',
        data: barData.category,
        name: barData.xName,
        nameLocation: 'middle',
        nameGap: 30,
        nameTextStyle: {
          fontWeight: 'bold'
        }
      },
      yAxis: {
        type: 'value',
        name: barData.yName,
        nameLocation: 'middle',
        nameGap: 60,
        nameTextStyle: {
          fontWeight: 'bold'
        }
      
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
    interface ScatterData {
      titleText: string;
      xName: string;
      yName: string;
      series: Array<ScatterSeriesOption>;
    }
    
    type ScatterOption = ComposeOption<EChartsBaseOption | ScatterSeriesOption>
    const scatterData: ScatterData = props.data as ScatterData
    console.log(scatterData.series)
    const scatterOption: ScatterOption = {
      title: {
        text: scatterData.titleText,
        left: 'center',
      }, 
      xAxis: {
        name: scatterData.xName,
        nameLocation: 'middle',
        nameGap: 30,
        nameTextStyle: {
          fontWeight: 'bold'
        }
      },
      yAxis: {
        name: scatterData.yName,
        nameLocation: 'middle',
        nameGap: 60,
        nameTextStyle: {
          fontWeight: 'bold'
        }
      },
      legend: {
        data: scatterData.series.map(seriesOption => (seriesOption.name as string)),
        right: 10,
      },
      series: scatterData.series 
    }

    option.value = scatterOption
    break
  case 'pie':
    use([PieChart])
    interface PieData {
      category: Array<string>;
      series: Array<PieSeriesOption>;
    }
    
    type PieOption = ComposeOption<EChartsBaseOption | PieSeriesOption>
    const pieData: PieData = props.data as PieData
    const pieOption: PieOption = {

    }

    option.value = pieOption
    break
  case 'line':
    use([LineChart])
    interface LineData {
      category: Array<string>;
      series: Array<LineSeriesOption>;
    }
    
    type LineOption = ComposeOption<EChartsBaseOption | LineSeriesOption>
    const lineData: LineData = props.data as LineData
    const lineOption: LineOption = {

    }

    option.value = lineOption
    break 

  default:
    console.log("Chart type not supported!")
    break
}

</script>

<style scoped>
v-chart {
  height: 100%;
  width: 100%;
}
</style>
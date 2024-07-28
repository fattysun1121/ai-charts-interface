<script setup lang="ts">
import { ref, computed, provide } from 'vue'
import { use } from 'echarts/core'
import { BarChart } from 'echarts/charts'
import { CanvasRenderer } from 'echarts/renderers'
import { 
  TitleComponent,
  GridComponent,
  TooltipComponent,
  LegendComponent } from 'echarts/components'


use([
  BarChart,
  TitleComponent,
  TooltipComponent,
  GridComponent,
  LegendComponent,
  CanvasRenderer
])


const input = ref('')

const options = ref({
  textStyle: {
    fontFamily: 'Inter, "Helvetica Neue"'
  },
  title: {
    text: 'Weekly Sales',
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
    type: 'bar',
    showBackGround: true,
    backgroundStyle: {
      color: 'rgba(180, 180, 180, 0.2)'
    }
  }

})
const output = computed(() => (input.value))

function update(e: Event) {
  input.value = (e.target! as HTMLInputElement).value
}

</script>

<template>
  <div id="container">
    <header>
      <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
    </header>

    <main>
      <div class="editor">
        <textarea :value="input" class="input"  @input="update" placeholder="Chart input:"></textarea>
        <div class="output">
          <v-chart :option="options" autoresize/>
        </div>
        
      </div>
    </main>
  </div>
</template>

<style scoped>
#container {
  position: absolute;
  right: 0;
  left: 0;
  top: 0;
  bottom: 0;
  display: flex;
  flex-direction: column;
  align-items: center;
  background-color: aliceblue;
}

.editor {
  height: 60rem;
  width: 80rem;
  display: flex;

}

.input,
.output {
  overflow: auto;
  height: 100%;
  box-sizing: border-box;
  padding: 20px;
}

.input {
  border: 1px solid #ccc;
  resize: none;
  outline: none;
  background-color: #f6f6f6;
  font-size: 14px;
  font-family: 'Monaco', courier, monospace;
  padding: 20px;
  width: 30rem;
}
.output {
  border: 1px solid #ccc;
  width: 50rem;
}
</style>

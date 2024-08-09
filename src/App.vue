<script setup lang="ts">
import { ref } from 'vue'


import ChartContainer from './components/ChartContainer.vue'


const input = ref('')
const option = ref(null)  // Doesn't do anything right here

const data = {
  titleText: 'Hello World!',
  category: ['MON', 'TUE', 'WED', 'THR', 'FRI', 'SAT', 'SUN'],
  series: [
    {
      name: 'Sales1',
      data: ['30000', '40000', '50000', '10000', '5000', '7900', '4500'],
      type: 'bar',
    },
    {
      name: 'Sales2',
      data: ['3000', '50000', '500', '20', '5023', '73900', '700'],
      type: 'bar',
    }
  ],
  xName: 'Weekday',
  yName: 'USD'
}

const scatterData = {

}

function update(e: Event) {
  input.value = (e.target! as HTMLInputElement).value
}

function generateChart(e: Event) {
  option.value = JSON.parse(input.value)
  console.log(option)
}

</script>

<template>
  <div id="container">
    <header>
      <img alt="Vue logo" class="logo" src="./assets/logo.svg" width="125" height="125" />
    </header>

    <main>
      <div class="editor">
        <div class="input-area">
          <div class="input-buttons">
            <button @click="input=''">Clear</button>
            <button @click="generateChart">Generate Chart</button>
          </div>
          
          <textarea :value="input" class="input"  @input="update" placeholder="Chart input:"></textarea>
        </div>
        
        <div class="output">
          <!-- <v-chart :option="options" autoresize/> -->
           <ChartContainer titleText="Hello World!" :data="data" chartType="bar" />
        </div>
        
      </div>
    </main>
  </div>
</template>

<style scoped>
.input-area {
  display: flex;
  flex-direction: column;
}
.input-buttons {
  display: flex;
  justify-content: space-around;
  border: 1px solid #ccc;
}

button {
  /* Remove default styling */
  background: none;
  color: inherit;
  border: none;
  padding: 0;
  font: inherit;
  cursor: pointer;
  outline: inherit;

  /* Add personal styling */
  font-size: 1rem;
  font-family: 'Monaco', courier, monospace;
  background-color: rgb(102, 206, 139);
  padding: 0.5rem 1rem 0.5rem 1rem;
  margin: 1rem;
  border-radius: 1.5rem;

}
button:hover {
  filter: brightness(120%);
}

button:active {
  box-shadow: inset 2px 2px 10px #222f28;
}

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
  height: 40rem;
  width: 80rem;
  display: flex;
}

.input,
.output {
  overflow: auto;
  height: 100%;
  box-sizing: border-box;
  padding: 20px;
  border: 1px solid #ccc;
}

.input {
  resize: none;
  outline: none;
  background-color: #f6f6f6;
  font-size: 14px;
  font-family: 'Monaco', courier, monospace;
  padding: 20px;
  width: 30rem;
}
.output {
  width: 50rem;
}
</style>

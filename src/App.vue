<script setup lang="ts">
// import { debounce } from 'lodash-es'
import { ref, computed } from 'vue'

const input = ref('')

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
        <div class="output" v-html="output"></div>
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

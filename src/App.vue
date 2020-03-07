<template>
  <div id="app">
    <div class="title">
      <h1>Calculator</h1>
    </div>
    <Calculator/>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue'

export default {
  name: 'App',
  components: {
    Calculator
  }
}
</script>

<style>
body {
  background-color: lightgray;
}

h1 {
  font-size: 50px;
  font-family:'Times New Roman', Times, serif;
}

.title {
  display: flex;
  align-items: center;
  justify-content: center;
  border: 2px solid black;
  border-radius: 10px;
  margin-bottom: 50px;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

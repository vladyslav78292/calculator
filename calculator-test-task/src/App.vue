<script>
  import Calculator from './components/Calculator.vue';
  export default {
    components: {
      Calculator
    } 
  }
</script>

<template>
  <div class="main">
    <Calculator />
  </div>
</template>

<style>
  body {
    background-color: black;
    margin: 0;
    padding: 0;
    box-sizing: border-box;
  }

  .main {
    font-family: Helvetica;
  }
</style>

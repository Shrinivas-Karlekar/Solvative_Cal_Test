<template>
  <div class="container">
    <div class="row">
      <div class="col">
        <Calculator></Calculator>
      </div>
      <div class="col">
        <History></History>
      </div>
    </div>
  </div>
</template>

<script>
import Calculator from './components/Calculator.vue';
import History from './components/History.vue';

export default {
  name: 'App',
  components: {
    Calculator,
    History
  }
}
</script>

<style>
.container {
  background-color: lightgrey;
}
</style>

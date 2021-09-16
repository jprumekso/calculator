<template>
  <div class="main">
    <calculator></calculator>
  </div>
</template>

<script>
import Calculator from '@/components/Calculator.vue';

export default {
  name: 'Home',
  components: {
    Calculator,
  },
};
</script>

<style>
  .main {
    max-width: 240px;
  }
</style>

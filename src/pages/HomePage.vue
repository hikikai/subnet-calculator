<template>
  <header :class="$style.header">
  <h1>Калькулятор подсетей</h1>
</header>  
<div>
<UiCalculator></UiCalculator>
</div>
</template>

<script setup lang="ts">
import UiCalculator from '../components/UiCalculator.vue';
</script>

<style module lang="scss">

.header{
  text-align: center;
  background-color: var(--color-gray-dark);
  width: 100%;
  height: 50px;
  font-size: 1rem;
  line-height: 1.5;
  padding: 5px;
  box-shadow: 0px 5px 25px -10px var(--color-gray-darkest) inset;
  flex-wrap: wrap;
}
</style>

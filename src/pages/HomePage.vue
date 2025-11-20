<template>
<header :class="$style.header">
  <h1>Калькулятор подсетей</h1>
</header>  


<div :class="$style.main">
  <div :class="$style.date">
    <div>
    <UiField :label="'IP-адрес'"></UiField>
    <UiInput v-model="inputV" :placeholder="'Введите IP'"></UiInput>
    </div>
    <div>
    <UiField :label="'Маска подсети'"></UiField>
    <UiSelect v-model="selectV" :options="maskList"></UiSelect>  
    </div>
  </div>
  <UiButton layout="primary">Подсчитать</UiButton>
</div>
</template>

<script setup lang="ts">
import { UiButton } from 'subnet-calculator-ui';
import { UiField } from 'subnet-calculator-ui';
import { UiSelect } from 'subnet-calculator-ui';
import { UiInput } from 'subnet-calculator-ui';
import { ref } from 'vue';

const maskList = ["255.255.255.255","255.255.255.254","255.255.255.252","255.255.255.248","255.255.255.240",
                  "255.255.255.224","255.255.255.192","255.255.255.128","255.255.255.000","255.255.254.000",
                  "255.255.252.000","255.255.248.000","255.255.240.000","255.255.224.000","255.255.192.000",
                  "255.255.128.000","255.255.000.000","255.254.000.000","255.252.000.000","255.248.000.000",
                  "255.240.000.000","255.224.000.000","255.192.000.000","255.128.000.000","255.000.000.000",
                  "254.000.000.000","252.000.000.000","248.000.000.000","240.000.000.000","224.000.000.000",
                  "192.000.000.000","128.000.000.000","000.000.000.000"]

const inputV = ref('0.0.0.0')
const selectV = ref('255.255.255.255')                  
</script>

<style module lang="scss">

//*{
//border: 2px solid black;
//}
.header{
  text-align: center;
  background-color: var(--color-gray);
  width: 100%;
  height: 50px;
  font-size: 1rem;
  line-height: 1.5;
  padding: 5px;
  box-shadow: 0px 5px 25px -10px var(--color-gray-darkest) inset
}

.main{
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  gap: 20px;
  min-height: calc(100vh - 600px);
}

.date{
  display: flex;
  gap: 10vh;
}
</style>
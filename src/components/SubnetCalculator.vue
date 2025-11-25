<template>



<form :class="$style.main" @submit.prevent="showResult">
  
  <div :class="$style.data">
    <div>
    <UiField :label="'IP-адрес'"></UiField>
    <UiInput v-model="ip" :placeholder="'Введите IP (0.0.0.0)'"></UiInput>
    </div>
    
    <div>
    <UiField :label="'Маска подсети'"></UiField>
    <UiSelect v-model="mask" :options="maskList"></UiSelect>  
    </div>
  </div>
  
  <UiButton type="submit" layout="primary" :disabled="!isIpValid(ip)">Рассчитать</UiButton>
  
  <div :class="$style.result" v-if="isShowResult && isIpValid(ip)">
    <div>IP: {{ ip }}</div>
    <div>Маска подсети: {{ mask }}</div>
    <div>Адрес сети: {{ getNetworkAdress(ip, mask) }}</div>
    <div>Количество адресов: {{ getAddressesCount(mask) }}</div> 
  </div>
</form>
</template>

<script setup lang="ts">
import { UiButton } from 'subnet-calculator-ui';
import { UiField } from 'subnet-calculator-ui';
import { UiSelect } from 'subnet-calculator-ui';
import { UiInput } from 'subnet-calculator-ui';
import { ref } from 'vue';
import { maskList } from './arrays';

const ip= ref('')
const mask = ref(maskList[0])     

const isShowResult = ref(false) 

function showResult(){
  isShowResult.value = true;
}

function isIpValid(ip: string): boolean {
  return (
    /^(\d{1,3})\.(\d{1,3})\.(\d{1,3})\.(\d{1,3})$/.test(ip) &&
    ip.split('.').every((octet) => Number(octet) <= 255)
  );
}

function getNetworkAdress(ip: string, mask: string): string {
    const ipOctets = ip.split('.');
    const maskOctets = mask.split('.');
    const result = [];

    for (let i = 0; i < 4; i++) {
        result.push(Number(ipOctets[i]) & Number(maskOctets[i]));
    }

    return `${result[0]}.${result[1]}.${result[2]}.${result[3]}`;
}

function getAddressesCount(mask: string): number { 
  let binaryMask = ''; 
 
  for (const octet of mask.split('.')) { 
    binaryMask += Number(octet).toString(2).padStart(8, '0'); 
  } 
  const zeros = 32 - binaryMask.replaceAll('0', '').length; 
 
  if (zeros === 0) return 1; 
  if (zeros === 1) return 2; 
 
  return Math.pow(2, zeros) - 2; 
}    
</script>

<style module lang="scss">

*{
// border: 2px solid black;
}


.main{
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 20px;
   min-height: 94.5vh;
  background-color: var(--color-gray-light);
  margin: auto;
  width: 65%;
  padding-bottom: 30%;
  flex-wrap: wrap;
  padding: 40px 0; 
}

.data{
  display: flex;
  gap: 10vh;
  flex-wrap: wrap;
}

.result{
  background-color: var(--color-gray);
  margin-top: 75px;
  border: none;
  border-radius: 25px;
  padding: 20px;
  width: 100%;
  max-width: 400px;
  text-align: center;
}

</style>
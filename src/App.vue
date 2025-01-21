<script setup>
import { ref } from 'vue';

const calculate_change = ref(0);

function CalculateHours() {

  const watt_applicane = parseFloat(document.getElementById('power_appliance').value);
  const power_avaliable = parseFloat(document.getElementById('avaliable_power').value);

  if (isNaN(watt_applicane) || isNaN(power_avaliable) || watt_applicane <= 0 || power_avaliable <= 0) {
    alert('Please enter valid value.');
    return;
  }

  const watt_to_kW = watt_applicane / 1000;

  const hoursofUsage = power_avaliable / watt_to_kW;

  document.getElementById('resultText').textContent = `You can use the appliance for approximately ${hoursofUsage.toFixed(2)} hours with ${power_avaliable} kW of available power.`

}

function CalculatePower() {
  
  const power_usage = parseFloat(document.getElementById('power_usage').value);
  const hours = parseFloat(document.getElementById('hours').value);

  if (isNaN(power_usage) || isNaN(hours) || power_usage <= 0 || hours <= 0) {
    alert('Please enter valid value.');
    return;
  }

  const power = (power_usage * hours) / 1000;  

  document.getElementById('resultText').textContent = `Your power usage is ${power.toFixed(2)} kWh.`

}

function CalculatePowerBank() {
  
  const volt = parseFloat(document.getElementById('power_volt').value);
  const capacity = parseFloat(document.getElementById('capacity').value);
  const usage_watt = parseFloat(document.getElementById('usage_watt').value);

  if (isNaN(volt) || isNaN(capacity) || isNaN(usage_watt) || usage_watt<= 0 || volt <= 0 || capacity <= 0) {
    alert('Please enter valid value.');
    return;
  }

  // convert mAh to kWh
  const powerInkWh = ( capacity * volt) / (1000 * 1000);

  // convert W to kW
  const wattInkW = usage_watt / 1000;

  const usage_time = powerInkWh/wattInkW;
  
// convert  to KWh
  document.getElementById('resultText').textContent = `You can use the appliance for approximately ${usage_time.toFixed(2)} hours with ${capacity} mAh of available power at ${volt}V.`;

}


</script>

<template>
  <h1 class=" mt-3 text-2xl font-semibold text-center">Power Usage Calculator</h1>

  <div class="flex justify-center items-center space-x-3 mt-5">
    <button @click="calculate_change = 0" v-if="calculate_change == 0"
      class="rounded-md bg-gray-500 px-3 py-1 text-white">
      Hours of Usage
    </button>

    <button @click="calculate_change = 0" v-else="calculate_change != 0"
      class="rounded-md px-3 py-1 bg-green-500 text-white">
      Hours of Usage
    </button>

    <button @click="calculate_change = 1" v-if="calculate_change == 1"
      class="rounded-md bg-gray-500 px-3 py-1 text-white">
      Power of Usage
    </button>

    <button @click="calculate_change = 1" v-else="calculate_change != 1"
      class="rounded-md px-3 py-1 bg-green-500 text-white">
      Power of Usage
    </button>

    <button @click="calculate_change = 2" v-if="calculate_change == 2"
      class="rounded-md bg-gray-500 px-3 py-1 text-white">
      Power Bank
    </button>

    <button @click="calculate_change = 2" v-else="calculate_change != 2"
      class="rounded-md px-3 py-1 bg-green-500 text-white">
      Power Bank
    </button>

  </div>
  <!-- first form -->
  <div v-if="calculate_change == 0" class=" flex justify-center">
    <div class=" mt-10 p-5 shadow-xl border-gray-400 border-1 rounded-lg w-1/3">
      <h3 class="text-xl text-center">Calculate Usage Hours</h3>

      <div class="flex-col mt-3 w-full justify-start">
        <label for="power_appliance">Power Applicane(Watt)</label>
        <div class="flex justify-center items-center w-full space-x-2">
          <input class="border-gray-500 border-2 mt-2 p-2 w-full h-10 rounded-md" type="number"
            placeholder="Enter Power Appliance" name="power_appliance" id="power_appliance">
        </div>
      </div>

      <div class="flex-col mt-3 w-full justify-start">
        <label for="avaliable_power">Avaliable Power(kW)</label>
        <div class="flex justify-center items-center w-full space-x-2">
          <input class="border-gray-500 border-2 mt-2 p-2 w-full h-10 rounded-md" type="number"
            placeholder="Enter Avaliable Power" name="avaliable_power" id="avaliable_power">
        </div>
      </div>

      <div>
        <button class=" bg-green-500 w-full text-white my-5 rounded-md h-10" @click="CalculateHours()">Calculate Usage
          Hours</button>
      </div>

      <div class="flex-col mt-3 w-full justify-start">
        <p id="resultText"></p>
      </div>

    </div>
  </div>

  <!-- Second Form -->
  <div v-if="calculate_change == 1" class=" flex justify-center">
    <div class=" mt-10 p-5 shadow-xl border-gray-400 border-1 rounded-lg w-1/3">
      <h3 class="text-xl text-center">Power of Usage</h3>

      <div class="flex-col mt-3 w-full justify-start">
        <label for="power_usage">Power Applicane(Watt)</label>
        <div class="flex justify-center items-center w-full space-x-2">
          <input class="border-gray-500 border-2 mt-2 p-2 w-full h-10 rounded-md" type="number"
            placeholder="Enter Power Appliance" name="power_usage" id="power_usage">
        </div>
      </div>

      <div class="flex-col mt-3 w-full justify-start">
        <label for="hours">Usage Hours</label>
        <div class="flex justify-center items-center w-full space-x-2">
          <input class="border-gray-500 border-2 mt-2 p-2 w-full h-10 rounded-md" type="number"
            placeholder="Enter Usage Hours" name="hours" id="hours">
        </div>
      </div>

      <div>
        <button class=" bg-green-500 w-full text-white my-5 rounded-md h-10" @click="CalculatePower()">Calculate Power Usage
        </button>
      </div>

      <div class="flex-col mt-3 w-full justify-start">
        <p id="resultText"></p>
      </div>

    </div>
  </div>

  <!-- Third Form -->
  <div v-if="calculate_change == 2" class=" flex justify-center">
    <div class=" mt-10 p-5 shadow-xl border-gray-400 border-1 rounded-lg w-1/3">
      <h3 class="text-xl text-center">Power Bank</h3>

      <div class="flex-col mt-3 w-full justify-start">
        <label for="usage_watt">Usage Watt(Watt)</label>
        <div class="flex justify-center items-center w-full space-x-2">
          <input class="border-gray-500 border-2 mt-2 p-2 w-full h-10 rounded-md" type="number"
            placeholder="Enter Power Usage" name="usage_watt" id="usage_watt">
        </div>
      </div>

      <div class="flex-col mt-3 w-full justify-start">
        <label for="capacity">Power Bank Capacity(mAh)</label>
        <div class="flex justify-center items-center w-full space-x-2">
          <input class="border-gray-500 border-2 mt-2 p-2 w-full h-10 rounded-md" type="number"
            placeholder="Enter Power Bank Capacity" name="capacity" id="capacity">
        </div>
      </div>

      <div class="flex-col mt-3 w-full justify-start">
        <label for="power_volt">Power Bank(Volt)</label>
        <div class="flex justify-center items-center w-full space-x-2">
          <input class="border-gray-500 border-2 mt-2 p-2 w-full h-10 rounded-md" type="number"
            placeholder="Enter Power Volt" name="power_volt" id="power_volt">
        </div>
      </div>

      <div>
        <button class=" bg-green-500 w-full text-white my-5 rounded-md h-10" @click="CalculatePowerBank()"> Calculate Usage Time
        </button>
      </div>

      <div class="flex-col mt-3 w-full justify-start">
        <p id="resultText"></p>
      </div>

    </div>
  </div>

</template>

<style scoped></style>

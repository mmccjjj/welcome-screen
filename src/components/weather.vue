<script setup>
import {onMounted,ref, onUnmounted, defineProps}  from 'vue';
import sunny from '@/assets/weatherIcons/sunny.png';
import rain from '@/assets/weatherIcons/rain.png';
import halfHalf from '@/assets/weatherIcons/half-half.png';
import cloudy from '@/assets/weatherIcons/cloudy.png';

const weather= ref([]);
const token= import.meta.env.VITE_SRF_TOKEN;
let intervalId = null;
const props= defineProps({
    currentDate: "",
});


async function fetchWeathernData() {

try{
        const response = await fetch('https://api.srgssr.ch/srf-meteo/v2/forecastpoint/47.3587,8.5128', {
      method: 'GET',
      headers: {
        'Content-Type': 'application/json',
        'Authorization': `Bearer ${token}` 
      }
    });
    if (!response.ok) {
      throw new Error(`HTTP error! Status: ${response.status}`);
    }
    const data = await response.json();
    weather.value= data.days;
    console.log(data.days);

    
}catch (error){
        console.log(error)
}
}

function formatWeatherDate(weatherDate) {
  const date = new Date(weatherDate);
  const day = date.getDate().toString().padStart(2, '0');
  const month = (date.getMonth() + 1).toString().padStart(2, '0');
  const year = date.getFullYear();
  const newWeatherDate = `${day}.${month}.${year}`;
  return newWeatherDate;
}

onMounted(() => {
    fetchWeathernData();
    intervalId = setInterval(  fetchWeathernData, 2* 60* 60* 1000);
}),

onUnmounted(() => {
      if (intervalId) {
        clearInterval(intervalId);
        console.log('Intervall gestoppt mit ID:', intervalId);
      }
    });

</script>

<template>
       <div v-for="(item, index) in weather" :key="index">
          <div class="weather" v-if="formatWeatherDate(item.date_time) == currentDate">

            <img class="icon" v-if="item.SUN_H >= 6 && item.PROBPCP_PERCENT <= 10" :src="sunny">
            <img class="icon" v-else-if="item.SUN_H >= 3 && item.PROBPCP_PERCENT <= 10" :src="cloudy">
            <img class="icon" v-else-if="item.SUN_H < 3 && item.PROBPCP_PERCENT <= 10" :src="halfHalf">
            <img class="icon" v-else-if="item.SUN_H < 3 && item.PROBPCP_PERCENT > 10" :src="rain">
            <img class="icon" v-else :src="halfHalf">
            
            <p>{{ item.TN_C }}</p>
            <p>{{ item.TX_C }}</p>

          </div>
       </div>
</template> 

<style scoped>

</style>
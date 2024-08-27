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

            <ul>
              <li>min: {{ item.TN_C }}C°</li>
              <li>max: {{ item.TX_C }}C°</li>
            </ul>
          </div>
       </div>
</template> 

<style scoped>
.icon{
  max-width: 100px;
  height: auto;
}

.weather{
  margin-right: 60px;
  display: flex;
  flex-direction: row-reverse;
  gap: 30px;
  border-width: 4px;
  border-color: white;
  border-style: solid;
  border-radius: 10px;
  padding: 8px;
  background-color: rgba(255, 255, 255, 0.13);
  box-shadow: 
        6px 6px 10px rgba(0, 0, 0, 5),
        inset 0 2px 3px rgba(255, 255, 255, 0.8),
        inset 2px 0 3px rgba(255, 255, 255, 0.8);

}

ul{
  margin: auto 0 auto 0;
  transform: translateY(2.5px);
  color: white;
  font-weight: 800;
  font-size: 20px;
}
li{
  margin: 5px;
}

</style>
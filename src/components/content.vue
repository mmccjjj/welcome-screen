<script setup>
import {onMounted,ref, onUnmounted}  from 'vue';
import weather from '@/components/weather.vue'


const screenData= ref([]);
let intervalId = null;
const date= new Date();


async function fetchScreenData() {

    try{
            const googleApi= import.meta.env.VITE_GOOGLE_API_KEY
            const googleSheetId= import.meta.env.VITE_GOOGLE_SHEET_ID
            const response = await fetch(`https://sheets.googleapis.com/v4/spreadsheets/${googleSheetId}/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=${googleApi}`)
            const data = await response.json()
            screenData.value = data.valueRanges[0].values.slice(1)
    }catch (error){
            console.log(error)
    }
}


onMounted(() => {
  fetchScreenData();
  intervalId = setInterval(  fetchScreenData, 2* 60* 60* 1000);
});

onUnmounted(() => {
      if (intervalId) {
        clearInterval(intervalId);
        console.log('Intervall gestoppt mit ID:', intervalId);
      }
    });


const formatDate = (date) => {
  const tag = String(date.getDate()).padStart(2, '0');
  const monat = String(date.getMonth() + 1).padStart(2, '0');
  const jahr = date.getFullYear();
  return `${tag}.${monat}.${jahr}`;
};

const formattedDate= formatDate(date);

</script>

<template>
    <div>
        <p>{{formattedDate}}</p>
        <div  v-if="screenData" 
              v-for="(item, index) in screenData" :key="index" 
              class= "content" 
              :class="item[3] == 'Oppotunity, Räffelstrasse 12' ? 'in' : 'out'"
              >
            <ul>
                <li :class="item[3] == 'Oppotunity, Räffelstrasse 12' ? 'itemTimeIn' : 'itemTimeOut'"
                    class= "itemTime">{{ item[1] }}, {{ item[0] }}</li>
                <li class= "itemTitle">{{item[2]}}</li>
                <li class= "itemAdress">{{ item[3] }}</li>
            </ul>
            <weather :current-date="item[0]"/>
        </div>
    </div>
</template>

<style scoped>

ul{
  flex-grow: 1;
}

li{
  color: 
  #FFBFAB;
  font-size: 28px;
  font-weight: 900;
  margin-top: 8px;
}

.itemTime{
  margin-top: 0;
}

.itemTimeIn{
  color: #EB5E00;
}

.itemTimeOut{
  color: #0F05A0;
}

.itemAdress{
  font-weight: 500;
}

.content{
  height: 182px;
  width: auto;
  margin: 0 auto 40px auto;
  padding: 34.5px 0 0 35px;
  display: flex;

 
}



.in{

  background-color: #0F05A0;

}

.out{

  background-color: #EB5E00;
}

p{
  color: #9AA7B1;
  font-size: 62px;
  font-weight: 500;
  margin: 21px 0 36px 0;
}

</style>
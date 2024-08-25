<script setup>
import {onMounted,ref}  from 'vue';

const screenData= ref([]);

async function fetchScreenData() {

    try{
            const response = await fetch('https://sheets.googleapis.com/v4/spreadsheets/1hzQjE8BH0Ilm8nam7sNRKRyAsd9akxQdKjLz4oBF8is/values:batchGet?ranges=A1%3AE100&valueRenderOption=FORMATTED_VALUE&key=AIzaSyBnkrLzmcWjKBf7TdGATCrf6SmpfKW_Kjw')
            const data = await response.json()
            screenData.value = data.valueRanges[0].values.slice(1)
            console.log(screenData.value);
    }catch (error){
            console.log(error)
    }
}

onMounted(() => {
  fetchScreenData()
})

const date= new Date();

const formatDate = (date) => {
  const tag = String(date.getDate()).padStart(2, '0');
  const monat = String(date.getMonth() + 1).padStart(2, '0');
  const jahr = date.getFullYear();
  return `${tag}.${monat}.${jahr}`;
};

const formattedDate= formatDate(date);

</Script>

<template>
    <div>
        <p>{{formattedDate}}</p>
        <div v-if="screenData" v-for="(item, index) in screenData" :key="index" :class="item[4] == 'Räffelstrasse' ? 'contentIn' : 'contentOut'">
            <ul>
                <li :class="item[4] == 'Räffelstrasse' ? 'itemTimeIn' : 'itemTimeOut'">{{ item[0] }}, {{ item[1] }}</li>
                <li class=" itemTitle">{{item[2]}}</li>
                <li class=" itemText">{{ item[3] }}</li>
            </ul>
        </div>
    </div>
</template>

<style scoped>

li{
  color: 
  #FFBFAB;
  font-size: 28px;
  font-weight: 900;
  margin-top: 8px;
}

.itemTimeIn{
  color: #EB5E00;
  margin-top: 0;
}

.itemTimeOut{
  color: #0F05A0;
  margin-top: 0;
}

.itemText{
  font-weight: 500;
}


.contentIn{
  height: 182px;
  width: 960px;
  background-color: #0F05A0;
  margin: 0 auto 40px auto;
  padding: 34.5px 0 0 35px;
}

.contentOut{
  height: 182px;
  width: 960px;
  background-color: #EB5E00;
  margin: 0 auto 40px auto;
  padding: 34.5px 0 0 35px;
}

p{
  color: #9AA7B1;
  font-size: 62px;
  font-weight: 500;
  margin: 21px 0 36px 60px;
}

</style>
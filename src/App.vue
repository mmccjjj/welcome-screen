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

</script>

<template>
  <div class="fullPage">
  <header>
    <h1>Welcome to Opportunity</h1>
  </header>

  <main>
    <p>{{formattedDate}}</p>
    <div class="content">
      <ul>
        <li class="itemTime"></li>
        <li class=" itemTitle">Basisbeschäftigung</li>
        <li class=" itemText">Interessierte für den zweiten Kurs werden uns besuchen</li>
      </ul>
    </div>
    <div class="content">
      <ul>
        <li class="itemTime">14.00 Uhr</li>
        <li class=" itemTitle">Basisbeschäftigung</li>
        <li class=" itemText">Interessierte für den zweiten Kurs werden uns besuchen</li>
      </ul>
    </div>
    <div class="content">
      <ul>
        <li class="itemTime">14.00 Uhr</li>
        <li class=" itemTitle">Basisbeschäftigung</li>
        <li class=" itemText">Interessierte für den zweiten Kurs werden uns besuchen</li>
      </ul>
    </div>
  </main>

  <footer>
    <img class="logoZh" src="@/assets/logos/STZH_SEB_Logo.png" alt="Logo" height="44">
    <img class="logoOp" src="@/assets/logos/Opportunity.png" alt="Logo" height="55">
    <img class="logoSa" src="@/assets/logos/SAG_Logo_De.png" alt="Logo" height="52">
  </footer>
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

.itemTime{
  color: #EB5E00;
  margin-top: 0;
}

.itemText{
  font-weight: 500;
}


.content{
  height: 182px;
  width: 960px;
  background-color: #0F05A0;
  margin: 0 auto 40px auto;
  padding: 34.5px 0 0 35px;
}

p{
  color: #9AA7B1;
  font-size: 62px;
  font-weight: 500;
  margin: 21px 0 36px 60px;
}

h1{
  font-size: 62px;
  font-weight: 900;
  margin: 69px 0 0 60px;
}

.fullPage{
  min-height: 100vh;
  display: flex;
  flex-direction: column;
}

main{
  /* flex: 1; */
  width: 100vw;
  height: 100vh;
}

footer{
  width: 100%;
  height: 130px;
  background-color: #FFFFFF;
  display: flex;
  align-items: center;
  padding-left: 40px;
  padding-right: 40px;
  
}

.logoOp{
 justify-self: center;
 margin-left: auto;
 margin-right: auto;
}

/* .logoSa{
  margin-left: auto;
  
} */

</style>

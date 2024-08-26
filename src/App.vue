<script setup>
import content from '@/components/content.vue'
import CstmFooter from '@/components/footer.vue'
</script>

<template>
  <div class="fullPage">
  <header>
    <h1>Welcome to Opportunity</h1>
  </header>

  <main>
    <content/>
  </main>

  <CstmFooter/>

</div>
</template>

<style scoped>
h1{
  font-size: 62px;
  font-weight: 900;
  margin: 69px 0 0 60px;
}

main{
  width: 100vw;
  min-height: 1920px;
  height: auto;
  padding: 0 60px 0 60px;
}

</style>

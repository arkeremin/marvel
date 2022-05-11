<template>
<div class="loader">
  Загрузка данных
</div> 
</template>

<script>
export default {
  name: 'showLoader',
}
</script>

<style>
.loader {
  display: flex; align-items: center; justify-content: center;
  width: 100%; height: 40vh;
  font-size: 55px; font-weight: bold; color: #ed171f;
  text-transform: uppercase; letter-spacing: 4px; text-align: center;
}
</style>
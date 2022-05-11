<template>
 <footer class="footer-wrap">
    <p>Домашняя работа</p>
    <!-- <p>НЕТОЛОГИЯ</p> -->
    <p>НЕТОЛОГИЯ<br/>Первые шаги в JavaScript: создаём сайт и приложение</p>
    <p>telegram: <a href="https://t.me/ARkER" target="_blank">@arker</a></p>
  </footer>
</template>

<script>
export default {
  name: 'showFooter',
  
}
</script>

<style>
.footer-wrap {
  display: block; margin: 20px 0 0; padding: 20px 15px;
  border-top: 2px solid var(--color-red);
}
.footer-wrap > p {font-size: 14px; letter-spacing: 0.5px; margin-bottom: 14px; color: var(--color-white);}
.footer-wrap > p > a {text-decoration: none; color: var(--color-red);}
.footer-wrap > p > a:hover {border-bottom: 2px solid var(--color-red);}

@media screen and (max-width: 1200px){ 
  .footer-wrap > p {font-size: 11px;}
}
</style>
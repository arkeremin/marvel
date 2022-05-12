<template>
<header class="header-wrap">
  
  <div class="header-logo">
    Marvel
  </div>
  
  <div class="header-search">
    <input  type="search"
            placeholder="Кого мы ищем ?"
            v-model.trim="search"
            @input="heroSearch(search)"
            autofocus>
  </div>

</header>
</template>

<script>
export default {
  name: 'showHeader',
  props: ['heroSearch'],
  data() {
    return {
      search: '',
    }
  },
}
</script>

<style>
.header-wrap {
  display: flex; flex-direction: row;
  align-items: center; justify-content: space-between;
  height: 82px; margin: 40px 50px 70px;
}
.header-logo {
  display: flex; align-items: center; justify-content: center;
  width: 320px; height: 100%;
  background-color: var(--color-red); color: var(--color-white);
  font-size: 50px; font-weight: 900;
  text-transform: uppercase; text-align: center;
}
.header-search {display: block;}
.header-search > input {
  background-color: var(--color-grey); color: var(--color-white);
  outline: none; border: none;
  font-size: 24px; text-align: right;
  padding: 0 6px 10px; border-bottom: 2px solid var(--color-red);
}
.header-search > input::-webkit-input-placeholder {
  font-size: 20px; color: #7c7b7e; text-align: left;
}
input[type="search"]::-webkit-search-decoration,
input[type="search"]::-webkit-search-cancel-button,
input[type="search"]::-webkit-search-results-button,
input[type="search"]::-webkit-search-results-decoration {-webkit-appearance:none;}

@media screen and (max-width: 1200px){ 
  .header-wrap {flex-direction: column; margin: 0 0 40px; height: auto;}
  .header-logo {width: 100%; padding: 12px 0;}
  .header-search {margin-top: 30px;}
  .header-search > input {text-align: center;}
}
</style>
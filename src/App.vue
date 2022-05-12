<template>

<!-- Модальное окно: Данные о герое -->
<ShowModal
  v-if="heroModalShow"
  @close="heroModalShow = false"
  :heroData="Heroes[heroID]"
/>

<!-- Главный макет -->
<div class="page-wrap">

  <!-- Заголовок: лого и поиск -->
  <ShowHeader :heroSearch="heroSearchData"/>

  <!-- Ждём данные -->
  <ShowLoader v-if="loading"/>

  <!-- DEbug -->
  <!-- <div class="debug"><pre>Ищем: {{search}}</pre></div> -->
  <div class="debug"><pre>{{heroesFilter}}</pre></div>

  <!-- Основной контент: вывод данных -->
  <main class="main-wrap">
  
  <section v-for="(hero, index) in Heroes" 
      :key = "hero.id"
      :class = "'hero id-' + index"
      @click = "heroID=index, heroModalShow=true, scroller()">

      <div class="polaroid"
        :style="randDeg(-6,6)">
      
        <div class="hero-photo">
          <img :src="hero.thumbnail" :alt="hero.name">
        </div>
      
        <div class="hero-name">
          {{hero.name}}
        </div>
      
      </div>

  </section>

  </main>
  <!-- /Основной контент: данные -->

  <!-- Подвал -->
  <ShowFooter/>

</div>

</template>

<script>
import ShowHeader from "./components/showHeader.vue";
import ShowLoader from "./components/showLoader.vue";
import ShowModal  from "./components/showModal.vue";
import ShowFooter from "./components/showFooter.vue";

export default {

  name: 'App',
  
  components: {
    ShowHeader,
    ShowLoader,
    ShowModal,
    ShowFooter,
  },

  data() {
    return {
      loading: false,
      heroModalShow: false,
      Heroes: undefined,
      heroID: 0,
      search: '',
      test: 'red',
    }
  },

  methods: {
    
    arrHeroes: function() {
      return fetch('https://netology-api-marvel.herokuapp.com/characters')
      .then(res => res.json())
      .then(json => this.Heroes = json)
    },

    heroSearchData: function(value) {
      this.search = value
    },

    randDeg: function (min, max) {
      min = Math.ceil(min)
      max = Math.floor(max)
      let valueDeg = Math.floor(Math.random() * (max - min + 1)) + min
      let classDeg = 'transform: rotate(' + valueDeg + 'deg);'
      return classDeg
    },

    scroller: function () {
      document.body.classList.toggle('body-scroll-off')
    },

  },

  computed: {
    heroesFilter: function () {
      let search = this.search
      return console.log (search)
    },

  },

  async mounted() {
    console.clear()
    console.log('Start APP')
    this.loading = true
    await this.arrHeroes()
    this.loading = false
  },
 
}
</script>

<style>
@import url('https://fonts.googleapis.com/css?family=Roboto+Condensed');
@import url('https://fonts.googleapis.com/css2?family=Caveat:wght@700&display=swap');

* {margin: 0; padding: 0;}

body::-webkit-scrollbar,
.modal-body-content::-webkit-scrollbar
  {width: 4px;}
body::-webkit-scrollbar-track,
.modal-body-content::-webkit-scrollbar-track
  {background-color: #a9a9a9;}
body::-webkit-scrollbar-thumb,
.modal-body-content::-webkit-scrollbar-thumb
  {box-shadow: inset 0 0 6px var(--color-red);}

:root {
  --color-grey:   #151515;
  --color-white:  #ffffff;
  --color-red:    #ed171f;
  --color-blue:   #1a73e8;
  --color-green:  #89c371;
}

html, body {font-family: 'Roboto', sans-serif;}
body {background-color: var(--color-grey); color: var(--color-white);}

.page-wrap {display: block; width: 1200px; margin: 0 auto;}
.debug {background-color: var(--color-red); color: var(--color-white);}

/* MAIN PAGE */
.main-wrap {display: flex; flex-flow: row wrap; justify-content: space-evenly; align-items: center;}
.hero {
  display: flex; flex-direction: column;
  cursor: pointer; 
  margin: 10px 30px 60px; padding: 0; width: auto;
}
.polaroid {
  color: var(--color-grey); background-color: var(--color-white);
  padding: 12px 12px 0 12px;
  filter: grayscale(100%);
  transform: scale(0.65, 0.65);
  transition: all 0.3s;
}
.polaroid:hover {
  filter: none;
  transform: scale(1.1, 1.1) rotate(0deg) !important;
  transition: all 0.3s;
}
.hero-photo {display: block;}
.hero-photo > img {display: block; width: 170px; height: 170px;}
.hero-name {
  display: flex; align-items: center; justify-content: center;
  width: 100%; height: 50px;
  font-family: 'Caveat', cursive;
  font-size: 13px; text-transform: uppercase;
}
/* /MAIN PAGE */

/* MOBILE */
@media screen and (max-width: 1200px){ 
  .page-wrap {width: auto;}
  .polaroid {filter: none; transform: scale(1, 1);}
}
</style>
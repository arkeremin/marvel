<template>
<transition name="modal">
<div class="modal-wrap">
  <div class="modal-body">

    <div class="modal-body-header">
        <h1>{{heroData.name}}</h1>
    </div>
    
    <div class="modal-body-content">  
      
      <div class="modal-hero-bio-photo">
        <div class="modal-polaroid">
         <img :src="heroData.thumbnail" :alt="heroData.name">
          <div class="modal-polaroid-caption">
            <span class="modal-polaroid-caption-name">{{heroData.name}}</span>
            <span class="modal-polaroid-caption-date">{{heroData.modified}}</span>
          </div>
        </div>
      </div>

      <div class="modal-hero-bio-text">
        <p>{{heroData.description}}</p>
        <h2>Был замечен в комиксах:</h2>
        <ul>
          <li v-for="comic in heroData.comics" :key="comic">
          {{comic.name}}
        </li>
      </ul>
      </div>

    </div>

    <div class="modal-body-footer">
      <button @click="$emit('close'), scrollerM()" class="modal-close">
          Закрыть досье
      </button>
    </div>
  
  </div>
</div>
</transition>
</template>

<script>
export default {
  name: 'showModal',   
  props: {
    heroData: Object,
  },
  methods: {
     scrollerM: function () {
      document.body.classList.toggle('body-scroll-off')
    },
  },
}
</script>

<style>
.modal-scroll {overflow: auto;}

.modal-wrap{
  background-color: rgba(2, 13, 47, 0.5);
  z-index: 9999;
  position: fixed; top: 0; left: 0; 
  display: flex; flex-direction: column;
  align-items: center; justify-content: center;
  margin: 0; width: 100vw; height: 100vh;
}
.modal-body {
  background-color: #000; color: var(--color-white);
  display: flex; flex-direction: column;
  width: 70vw; padding: 0;
  border: 2px solid var(--color-green); border-radius: 1px;
}

.modal-body-header {display: block;}
.modal-body-header > h1 {
  font-size: 30px; text-transform: uppercase;
  background-color: var(--color-red); display: inline-block;
  padding: 8px 25px; margin-bottom: 25px;
  margin: 25px 0 20px 30px; 
}

.modal-body-content {
  display: flex; flex-direction: row-reverse;
  overflow-x: hidden;
  overflow-y: auto; height: 50vh;
  margin-bottom: 20px; width: auto;
}

.modal-hero-bio-text {
  display: block; width: 75%; padding: 0 30px;
}
.modal-hero-bio-text > p {font-size: 18px; margin-bottom: 15px; text-align: justify;}
.modal-hero-bio-text > h2 {font-size: 16px; margin: 20px 0 10px;}
.modal-hero-bio-text > ul {padding-left: 10px;}
.modal-hero-bio-text > ul > li {font-size: 10px; margin-bottom: 6px;}

.modal-hero-bio-photo {
  display: block; width: 30%; padding-right: 30px;
}
.modal-polaroid {
  background-color: var(--color-white); padding: 20px 20px 0;
}
.modal-polaroid > img {
  max-width: 100%; height: auto;
}
.modal-polaroid-caption {
  color: #000; width: 100%; height: auto; padding: 25px 0;
  display: flex; align-items: center; justify-content: space-between; flex-direction: column;
}
.modal-polaroid-caption-name {
  font-family: 'Caveat', cursive;
  font-size: 24px; text-transform: uppercase;
  margin-bottom: 10px;
}
.modal-polaroid-caption-date {font-size: 8px; text-align: right; width: 100%;}

.modal-body-footer {display: block; text-align: center; margin: 30px 0 20px;}
.modal-close {
  color: var(--color-white); background-color: var(--color-red);
  margin: 0; padding: 15px 35px;
  font-size: 14px; text-transform: uppercase; letter-spacing: 0.1px;
  border: none; outline: none; cursor: pointer;
  clip-path: polygon(8% 0, 100% 0, 100% 65%, 92% 100%, 0 100%, 0 35%);  
}
.modal-close:hover {background-color: #9f0013;}

/* MOBILE */
@media screen and (max-width: 1200px){ 
  /* .modal-wrap {} */
  .modal-body {
    padding: 0; width: 80vw;
    border-color: var(--color-white);
  }
  .modal-body-header {display: none;}
  .modal-body-content {
    flex-direction: column;
    padding: 0; margin: 0; height: 60vh;
  }
  .modal-hero-bio-text {width: auto; padding: 20px 8px 0;}
  .modal-hero-bio-text > p {font-size: 17px; text-align: left;}
  .modal-hero-bio-photo {width: auto; padding: 0;}
  .modal-close {margin-bottom: 20px;}
}
</style>
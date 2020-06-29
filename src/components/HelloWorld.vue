<template>
  <section class="gallery">
    <h1 class="gallery__title">{{ msg }}</h1>
    <input type="text" id="search" class="gallery__input" placeholder="Search Photos" v-model="query">
    <button @click="searchPhotos" class="gallery__btn">Search </button> 
    <div class="lds-roller" v-if="isLoading"><div></div><div></div><div></div><div></div><div></div><div></div><div></div><div></div></div>
    <stack
              :column-min-width="300"
              :gutter-width="15"
              :gutter-height="15"
              monitor-images-loaded
      >
        <stack-item
                v-for="(item, index) in resultArr"
                :key="index"
                style="transition: transform 300ms"
        >
          <img :src="item.urls.small" :alt="item.alt_description" class="gallery__img"/>
        </stack-item>
      </stack>
     
  </section>
</template>

<script>

import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
import { Stack, StackItem } from "vue-stack-grid";
 
Vue.use(VueAxios, axios)


export default {
  
  name: 'HelloWorld',
  props: {
    msg: String
  },
  components: { Stack, StackItem },
   data() {
    return {
      query: "",
      resultArr: [],
      myID: "JI3Cv0kZH--WLhr9PFVuiHyO5xnVubQzNswGcSP5LD8",
      isLoading: false,
    }
  },
  methods: {searchPhotos() {
  const promise1 = new Promise((resolve, reject) => {
   
   try{
      const response = Vue.axios.get(`https://api.unsplash.com/search/photos?query=${this.query}&per_page=30&client_id=${this.myID}`)
    
      if(response){
        setTimeout(() => {
            resolve(response)
        }, 3000)
      }

    
    } catch(error){
      reject(error)
    }
    this.isLoading = true
});

promise1.then((response) => {
     this.isLoading = false
  if(response) {
    this.resultArr = response.data.results.map(item => {
      return item
    })
  }
});
}}
}
</script>

<style lang="scss">
@import "./_default.scss";
  @import "./_HelloWorld.scss";
  @import "./Loader.scss";
</style>

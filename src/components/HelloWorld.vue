<template>
  <div class="hello">
    <h1>{{ msg }}</h1>
    <input type="text" id="search" placeholder="Search Photos" v-model="query">
    <button @click="searchPhotos">Search</button> 
    <!-- <div id="result"></div> -->
    <span v-if="isLoading">huy</span>
    <div class="result__container" v-if="resultArr && resultArr.length">
      <img :src="item.urls.regular" alt="" v-for="(item, index) in resultArr" :key="index">
    </div>
  </div>
</template>

<script>

import Vue from 'vue'
import axios from 'axios'
import VueAxios from 'vue-axios'
 
Vue.use(VueAxios, axios)


export default {
  name: 'HelloWorld',
  props: {
    msg: String
  },
   data() {
    return {
      query: "",
      resultArr: [],
      myID: "JI3Cv0kZH--WLhr9PFVuiHyO5xnVubQzNswGcSP5LD8",
      isLoading: false
    }
  },
  methods: {searchPhotos() {
  const promise1 = new Promise((resolve, reject) => {
    this.isLoading = true
   try{
      const response = Vue.axios.get(`https://api.unsplash.com/search/photos?query=${this.query}&client_id=${this.myID}`)
    
      if(response){
        resolve(response)
      }

    
    } catch(error){
      reject(error)
    }
    this.isLoading = false
});

promise1.then((response) => {
  if(response) {
    this.resultArr = response.data.results.map(item => {
      return item
    })
  }
});
}}
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style >
h3 {
  margin: 40px 0 0;
}
ul {
  list-style-type: none;
  padding: 0;
}
li {
  display: inline-block;
  margin: 0 10px;
}
a {
  color: #42b983;
}

#result {
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
}

.img_preview {
  width: 300px;
  height: 300px;
}
</style>

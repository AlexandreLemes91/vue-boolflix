<template>
  <div id="app">
    <Header @search="getList" />

    <Content :videoList="videoList"/>
  </div>
</template>

<script>
import axios from 'axios';
import Header from '@/components/Header'
import Content from '@/components/Content'

export default {
  name: 'App',

  components: {
    Header,
    Content,
  },

  data(){
    return{
      // INFO PER CHIAMATA API
      apiURL: 'https://api.themoviedb.org/3/search/',
      key: '24bf6c82b0fc8353485988e42545f9c0',

      //ARRAY DI FILM E SERIE TV
      filmsList: [],
      seriesList: [],

      //ARRAY CHE CONTERRA' SIA FILM CHE SERIE TV
      videoList: [],
    }
  },

  methods: {
    //FUNZIONE PER CHIAMATA CUSTOM API TRAMITE $emit DA HEADER, POPOLERA' LA LISTA videoList
    getList(search){
      if( search !== ''){
        axios.all([
          //FILMS LIST
          axios.get(this.apiURL + 'movie', 
            {
              params: {
                api_key: this.key,
                query: search,
              }
            }),
  
          //SERIES LIST
          axios.get(this.apiURL + 'tv', 
            {
              params: {
                api_key: this.key,
                query: search,
              }
            })
        ])
        .then( responses =>{
          console.log(responses)
          this.filmsList = responses[0].data.results;
          this.seriesList = responses[1].data.results;
  
          //UNIONE DEGLI ARRAY <--- ricordarsi dell'assincronicità
          this.videoList = [...this.seriesList, ...this.filmsList];
          console.log(this.videoList);
        })
      }
    }
  }

}

</script>

<style lang="scss">
@import '@/components/scss/general';

</style>

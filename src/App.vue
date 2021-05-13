<template>
  <div id="app">
    <Header @search="getList" />

    <Content 
      :searchActive="searchActive"
      :videoList="videoList"
      :seriesList="seriesList"
      :filmsList="filmsList"
      :top10Movie="Top10Movie"/>
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
      searchActive: false,

      apiBestMovie: 'https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc',

      // INFO PER CHIAMATA API
      apiURLsearch: 'https://api.themoviedb.org/3/search/',
      key: '24bf6c82b0fc8353485988e42545f9c0',

      //ARRAY DI FILM E SERIE TV
      filmsList: [],
      seriesList: [],
      //TOP 10 MOVIE
      Top10Movie: [],

      //ARRAY CHE CONTERRA' SIA FILM CHE SERIE TV
      videoList: [],
    }
  },

  created(){
    this.get10BestMovie();
  },

  methods: {
    //FUNZIONE PER CHIAMATA CUSTOM API TRAMITE $emit DA HEADER, POPOLERA' LA LISTA videoList
    getList(search){
      const apiParams = {
        api_key: this.key,
        query: search,
        language: 'it-IT'
      };

      if( search !== ''){
        axios.all([
          //FILMS LIST
          axios.get(this.apiURLsearch + 'movie', {params: apiParams}),
  
          //SERIES LIST
          axios.get(this.apiURLsearch + 'tv', {params: apiParams})
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
      this.searchActive = true;
    },

    //FUNZIONE TOP 10 MOVIES
    get10BestMovie(){
      axios.get('https://api.themoviedb.org/3/discover/movie?sort_by=popularity.desc&api_key=24bf6c82b0fc8353485988e42545f9c0')
      .then(resp=>{
        for(let i=0; i<10; i++){
          this.Top10Movie.push(resp.data.results[i]);
        }
      })
      console.log(this.Top10Movie);
    },
  }

}

</script>

<style lang="scss">
@import '@/components/scss/general';

</style>

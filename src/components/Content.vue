<template>
    <main>
        <ul v-for="video in videoList" :key="video.id">
            <li>Title: {{video.title}}</li>
            <li>Original Title: {{video.original_title}}</li>
            <li>Language: {{video.original_language}}</li>
            <li>{{video.vote_average}}</li>
        </ul>
    </main>
</template>

<script>
import axios from 'axios';

export default {
    name: 'Content',

    data(){
        return{
            apiURL: 'https://api.themoviedb.org/3/search/movie?api_key=24bf6c82b0fc8353485988e42545f9c0&query=v for vendetta',
            videoList: [],
        }
    },

    created(){
        this.getList();
    },

    methods: {
        getList(){
            axios.get(this.apiURL)
            .then(resp=>{
                this.videoList = resp.data.results;
                console.log(this.videoList);
            })
        }
    }
}
</script>

<style>

</style>
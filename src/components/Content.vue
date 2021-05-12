<template>
    <main>

        <!-- QUESTO DIVENTERA UN COMPONENTE -->
        <div class="video" v-for="video in videoList" :key="video.id">
            <img :src="'https://image.tmdb.org/t/p/w342' + video.poster_path " alt="">
            <ul>
                <li>Title: {{video.title}}{{video.name}}</li> <!-- SI PUO FARE MEGLIO??? ANZICHE' QUESTA DOPPIA MUSTACHE -->
                <li>Original Title: {{video.original_title}}{{video.original_name}}</li>
                <li>Language: <img :src='flags(video.original_language)'  :alt="video.original_language"></li> <!-- <-------usare le back -->
                <li>{{video.vote_average}}</li>
            </ul>
        </div>
    </main>
</template>

<script>

export default {
    name: 'Content',
    props: ['videoList'],

    methods: {
        flags(videoLanguage){
            let img = '';
            switch(videoLanguage){
                case 'en':
                    img = require('@/assets/img/flags/en.png');
                    break;
                case 'it':
                    img = require('@/assets/img/flags/it.png');
                    break;
            }
            return img;
        }
    }
}
</script>

<style scoped lang='scss'>

li{
    img{
        max-width: 30px;
    }
}
</style>
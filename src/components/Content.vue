<template>
    <main>

        <!-- QUESTO DIVENTERA UN COMPONENTE -->
        <div class="video" v-for="video in videoList" :key="video.id">

            <!-- IMG VIDEO -->
            <img v-if="video.poster_path !== null" :src="'https://image.tmdb.org/t/p/w342' + video.poster_path " alt="">
            <div v-else class="imgSubstitute"><h2>{{video.title ? video.title : video.name}}</h2></div>

            <!-- LIST INFO -->
            <ul>
                <li>Title: {{video.title ? video.title : video.name}}</li>
                <li>Original Title: {{video.original_title ? video.original_title : video.original_name}}</li>
                <li>Language: 
                    <img v-if="flags(video.original_language)"
                        :src='require(`@/assets/img/flags/${video.original_language}.png`)'
                        :alt="video.original_language">
                    <span v-else>{{video.original_language}}</span>
                </li>
                <li>
                    <i v-for="(star, index) in getStars(video.vote_average)" :key="index + video.id" class="fullStar fas fa-star"></i>
                    <i v-for="(star, index) in 5 - getStars(video.vote_average)" :key="'emptyStar' + index + video.id" class="emptyStar fas fa-star"></i>
                </li>
            </ul>
        </div>
    </main>
</template>

<script>

export default {
    name: 'Content',
    props: ['videoList'],

    data(){
        return{
            flagsArray: [
                'it',
                'en',
            ]
        }
    },

    methods: {
        flags(videoLanguage){
            return this.flagsArray.includes(videoLanguage);
            /* let img = '';
            switch(videoLanguage){
                case 'en':
                    img = require('@/assets/img/flags/en.png');
                    break;
                case 'it':
                    img = require('@/assets/img/flags/it.png');
                    break;
            }
            return img; */
        },

        getStars(vote){
            return Math.round(vote / 2);
        }
    }
}
</script>

<style scoped lang='scss'>

.imgSubstitute{
    width: 342px;
    height: 513px;
    background-color: #999;
    display: flex;
    align-items: center;
    justify-content: center;
}

li{
    img{
        max-width: 30px;
    }

    .fullStar{
        color: orange;
    }
    .emptyStar{
        color: #999;
    }
}
</style>
<template>
    <div>
        <div class="video">

            <!-- IMG VIDEO -->
            <img v-if="info.poster_path !== null" :src="'https://image.tmdb.org/t/p/w185' + info.poster_path " alt="">
            <div v-else class="imgSubstitute"><h2>{{info.title ? info.title : info.name}}</h2></div>

            <!-- LIST INFO -->
            <!-- <ul>
                <li>Title: {{info.title ? info.title : info.name}}</li>
                <li>Original Title: {{info.original_title ? info.original_title : info.original_name}}</li>
                <li>Language: 
                    <img v-if="flags(info.original_language)"
                        :src='require(`@/assets/img/flags/${info.original_language}.png`)'
                        :alt="info.original_language">
                    <span v-else>{{info.original_language}}</span>
                </li>
                <li>
                    <i v-for="(star, index) in getStars(info.vote_average)" :key="index + info.id" class="fullStar fas fa-star"></i>
                    <i v-for="(star, index) in 5 - getStars(info.vote_average)" :key="'emptyStar' + index + info.id" class="emptyStar fas fa-star"></i>
                </li>
            </ul> -->
        </div>

    </div>
</template>

<script>
export default {
    name: 'Card',
    props: ['info'],

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
        },

        getStars(vote){
            return Math.round(vote / 2);
        }
    }
    
}
</script>

<style lang='scss' scoped>
.video{
    color: white;
    height: 272px;
    width: 185px;

    img{
        height: 272px;
        width: 185px;
        object-fit: cover;
    }
}


.imgSubstitute{
    width: 185px;
    height: 272px;
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
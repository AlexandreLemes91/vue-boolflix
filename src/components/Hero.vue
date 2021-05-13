<template>
    <section>
        <div class="layover"></div>
        <div class="infos">
            <div class="title">
                <h1>{{forHero.title ? forHero.title : forHero.name}}</h1>
            </div>

            <ul>
                <li>
                    <i v-for="(star, index) in getStars(forHero.vote_average)" :key="index + forHero.id" class="fullStar fas fa-star"></i>
                    <i v-for="(star, index) in 5 - getStars(forHero.vote_average)" :key="'emptyStar' + index + forHero.id" class="emptyStar fas fa-star"></i>
                </li>

                <li>Anno {{forHero.release_date.slice(0,4)}}</li>

                <li>
                    <img v-if="flags(forHero.original_language)"
                        :src='require(`@/assets/img/flags/${forHero.original_language}.png`)'
                        :alt="forHero.original_language">
                    <span v-else>{{forHero.original_language}}</span>
                </li>
            </ul>

            <div class="overview">{{forHero.overview}}</div>
        </div>
        <div class="img-container">
            <div class="layover-img"></div>
            <div class="layover-img"></div>
            <img :src="'https://image.tmdb.org/t/p/w780' + forHero.backdrop_path" alt="">
        </div>
    </section>
</template>

<script>
export default {
    name: 'Hero',
    props: ['forHero'],

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
        },
    },
}
</script>

<style scoped lang="scss">
@import '@/components/scss/var.scss';

section{
    display: flex;
    padding-left: 10px;
    position: relative;
    min-height: 400px;
    width: 100vw;

    .layover{
        position: absolute;
        height: 100%;
        width: 100%;
        background-image: linear-gradient(125deg, rgba($blackFlix,1), rgba(white, 0.05), rgba($blackFlix,0.15),transparent, transparent);
        z-index: -1;
    }

    .infos{
        width: 60%;
        margin-top: 50px;

        .title{
            max-width: 90%;
            h1{
                text-transform: uppercase;
                font-size: 28px;
            }
        }
    
        ul{
            display: flex;
            margin: 5px 0px 20px;
            font-size: 14px;
            li{
                margin-right: 15px;
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
        }
    
        .overview{
            width: 90%;
            line-height: 22px;
        }
    }

    .img-container{
        position: absolute;
        right: 0;
        z-index: -2;
        overflow: hidden;
        height: 439px;

        .layover-img{
            height: 100%;
            width: 100%;
            position: absolute;
            background-image: linear-gradient(to right, $blackFlix , rgba($blackFlix, 0));
        }
        img{
            height: 120%;
        }
    }

}

</style>
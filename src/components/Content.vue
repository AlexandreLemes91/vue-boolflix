<template>
    <main>
        <div class="layover"></div>
        
        <Hero
            v-if="searchActive === false"
            :forHero="clicked ? activeMovie : top10Movie[0]"/>

        <div class="top10Movie" v-if="searchActive === false">
            <h2>Top 10</h2>
            <div class="row">
                <div
                    class="card-container"
                    v-for="(movie,index) in top10Movie"
                    :key="movie.id"
                    @click="hero(movie)">

                    <Card :info="movie"/>

                    <div class="index">{{index + 1}}</div>
                </div>
            </div>
        </div>

        <div v-else class="search">
            <div
                class="card-container"
                v-for="movie in videoList"
                :key="movie.id">

                <Card :info="movie"/>
            </div>
        </div>

    </main>
</template>

<script>
import Hero from '@/components/Hero'
import Card from '@/components/Card'

export default {
    name: 'Content',
    props: ['videoList', 'seriesList', 'filmsList', 'top10Movie', 'searchActive'],

    components: {
        Hero,
        Card,
    },

    data(){
        return{
            activeMovie: this.top10Movie[0],
            clicked: false,
        }
    },

    methods: {
        hero(video){
            this.activeMovie = video;
            this.clicked = true
            console.log(this.activeMovie);
        },
    }
}
</script>

<style scoped lang='scss'>
@import '@/components/scss/var.scss';

main{
    color: white;
    
    .top10Movie{
        overflow-x: auto;
        height: 390px;
        margin-top: 30px;
        h2{
            margin-left: 10px;
        }
        .card-container{
            position: relative;
            margin: 10px;
            margin-right: 50px;
            transition: margin-right 0.5s;
            border: 2px solid transparent;
            &:hover .index{
                right: -70%;
            }
            &:hover{
                margin-right: 100px;
                border: 2px solid white
            }

            .index{
                z-index: -1;
                position: absolute;
                bottom: -25px;
                right: -50%;
                height: 100%;
                width: 100%;
                font-size: 300px;
                letter-spacing: -80px;
                line-height: 0px;
                display: flex;
                align-items: center;
                transition: 0.5s;
            }
        }
        
    }

    .search{
        display: flex;
        max-width: 100vw;
        flex-wrap: wrap;

        .card-container{
            margin: 5px;
            position: relative;
        }
    }
}

</style>
<template>
    <main>

        <Hero/>

        <div class="top10Movie">
            <h2>Top 10</h2>
            <div class="row">
                <div
                    v-for="(movie,index) in top10Movie"
                    :key="movie.id"
                    class="card-container"
                    @click="hero(movie)"
                    :hero="">

                    <Card :info="movie"/>

                    <div class="index">{{index + 1}}</div>
                </div>
            </div>
        </div>

    </main>
</template>

<script>
import Hero from '@/components/Hero'
import Card from '@/components/Card'

export default {
    name: 'Content',
    props: ['videoList', 'seriesList', 'filmsList', 'top10Movie'],

    components: {
        Hero,
        Card,
    },
    
    dat(){
        return{
            activeMovie: [],
        }
    },

    methods: {
        hero(video){
            console.log(video);
            this.
        },
    }
}
</script>

<style scoped lang='scss'>
@import '@/components/scss/var.scss';

main{
    color: white;
    
    .top10Movie{
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
}

</style>
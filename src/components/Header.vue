<template>
    <header>
        <div class="left">
            <img src="@/assets/img/lexflix.png" alt="">
            <nav>
                <ul>
                    <li v-for="link in nav" :key="link"><a href="/">{{link}}</a></li>
                </ul>
            </nav>
       </div>

        <div class="right">
            <form>
                <input :class="{'active' : activeInput}" type="text" v-model.trim="searching">
                <button
                    @click="openInput()"
                    @click.prevent="$emit( 'search', searching )">
                    <i class="fas fa-search"></i>
                </button>
            </form>
        </div>
    </header>
</template>

<script>
export default {
    name: 'Header',

    data(){
        return{
            searching: '',

            nav: [
                'home',
                'TV show',
                'movies',
                'latest',
                'my list'
            ],

            activeInput: false
        }
    },

    methods: {
        openInput(){
            this.activeInput = true
        }
    }
}
</script>

<style scoped lang='scss'>
@import '@/components/scss/var.scss';

header{
    display: flex;
    justify-content: space-between;
    align-items: center;
    color: $notFocusColor;
    background-color: $blackFlix;
    //canc
    padding: 10px 20px;
    //canc

    .left{
        display: flex;
        align-items: center;
        img{
            max-width: 150px;
            margin-right: 30px;
        }

        nav{
            ul{
                display: flex;
                text-transform: capitalize;
                li{
                    margin: 0 10px;
                    font-weight: 600;
                    &:hover{
                        color: white;
                    }
                }
            }
        }
    }

    .right{

        input{
            background-color: unset;
            border: unset;
            border-bottom: 1px solid $redFlix;
            width: 0;
            transition: width 0.8s;
            color: white;
            padding: 3px 0;
            &:focus{
                outline: none;
            }
            &.active{
                width: 180px;
            } 
        }

        button{
            color: white;
            background-color: unset;
            border: unset;
            margin-left: 5px;
        }
    }

}


</style>
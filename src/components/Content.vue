<template>
    <main>
        <ul v-for="video in videoList" :key="video.id">
            <li>Title: {{video.title}}{{video.name}}</li> <!-- SI PUO FARE MEGLIO??? ANZICHE' QUESTA DOPPIA MUSTACHE -->
            <li>Original Title: {{video.original_title}}{{video.original_name}}</li>
            <li>Language: <img :src="video.original_language == 'en' ? flags.en : flags.it" alt=""></li> <!-- tramite V-IF METTERE ALTRE LINGUE? OPPURE TRAMITE UNO SWITCH? -->
            <li>{{video.vote_average}}</li>
        </ul>
    </main>
</template>

<script>

export default {
    name: 'Content',
    props: ['videoList'],

    data(){
        return{
            flags: {
                en: require('@/assets/img/flags/en.png'),
                it: require('@/assets/img/flags/it.png'),
            }
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
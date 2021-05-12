<template>
    <header>
        <form>
            <input type="text" v-model.trim="searching">
            <button @click.prevent="$emit( 'search', searching )">Search</button>
        </form>
    </header>
</template>

<script>
export default {
    name: 'Header',

    data(){
        return{
            searching: '',
        }
    }
}
</script>

<style scoped lang='scss'>

header{
    background-color: #555;
    padding: 20px;
}


</style>
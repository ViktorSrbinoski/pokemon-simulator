<template>
    <img alt="Vue logo" src="./assets/logo.png" class="logo">
    <PokemonSimulator msg="Hello World"/>
</template>

<script>
    import PokemonSimulator from './components/PokemonSimulator.vue'

    export default {
        name: 'App',
        components: {
            PokemonSimulator
        }
    }
</script>

<style>
    #app {
        font-family: Avenir, Helvetica, Arial, sans-serif;
        -webkit-font-smoothing: antialiased;
        -moz-osx-font-smoothing: grayscale;
        text-align: center;
        color: #2c3e50;
        margin-top: 60px;
    }

    .logo {
        width: 10%;
        margin-bottom: 30px;
    }
</style>

<template>
  <div id="app">
    <MainApp/>
  </div>
</template>

<script>
import MainApp from './components/MainApp.vue'

export default {
    name: 'app',
    components: {
        MainApp
    },
    data() {
        return {
            abc:null
        }
    },
    methods: {
        cancel() {
            console.log('cancel nef')
        }
    },
    computed: {

    },
    mounted(){

    }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>

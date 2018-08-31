<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
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
        post.on('value', dataSnapshot => {
            console.log(dataSnapshot.val())
        });
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
  margin-top: 60px;
}
</style>

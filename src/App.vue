<template>
  <div id="app">
    <img alt="Vue logo" src="./assets/logo.png">
    <MainApp/>

  </div>
</template>

<script>
import MainApp from './components/MainApp.vue'
let config = {
apiKey: "AIzaSyBa52ClshRaZashVd8U79FClWDBd2Rfi7o",
authDomain: "demorealtimedatabase-a4ba2.firebaseapp.com",
databaseURL: "https://demorealtimedatabase-a4ba2.firebaseio.com",
projectId: "demorealtimedatabase-a4ba2",
storageBucket: "demorealtimedatabase-a4ba2.appspot.com",
messagingSenderId: "523187674313"
};
const appF = firebase.initializeApp(config);
const dbF = appF.database();
const post = dbF.ref('posts');

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

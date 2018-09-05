<template>
    <div>
        <div class="w-30">sidebar
            <ul>
                <li v-for="(days,keyMontth) in months" :key="keyMontth">
                    <a class="collapsible" href="#">{{keyMontth}}</a>
                    <ul class="list">
                        <li v-for="(day,key) in days" :key="key">
                            <a href="#">{{day}}</a>
                        </li>
                    </ul>

                </li>
            </ul>
        </div>
        <div class="">main</div>
    </div>
</template>
<script>
    export default{
        name: 'MainAppNe',
        props:{
        },
        data(){
            return {
                months : {
                    '2018-08' : ['01','02','03'],
                    '2018-09' : ['01','02','03']
                }
            }
        }
    }
</script>
<style lang="css">
    ul{
        text-align: left;
        list-style: none;
    }
    .w-30{
        width: 30%;
    }
    .collapsible {
      background-color: #777;
      color: white;
      padding: 18px;
      width: 100%;
      display: block;
    }
    .collapsible:after {
      content: '\002B';
      color: white;
      font-weight: bold;
      float: right;
      margin-left: 5px;
    }
    .active:after {
      content: "\2212";
    }
</style>
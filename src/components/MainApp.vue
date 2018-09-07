<template>
    <div class="d-flex">
        <div class="w-90 t-left d-flex">
            <div class="w-100p d-in t-right"><label for="word">WORD </label></div> <input id="word" class="w-40" type="text" name=""/>
            <label for="mean">MEAN </label> <input id="mean" class="w-40" type="text" name=""/><br/><br/>
            <label for="explain">EXPLAIN </label> <textarea id="explain" class="w-90" type="text" name=""></textarea>
        </div>
        <button class="btn">Add word</button>
        <div class="w-30">
            <ul>
                <li v-for="(days,keyMontth) in months" :key="keyMontth">
                    <a class="collapsible" href="#">{{keyMontth}}</a>
                    <ul class="list">
                        <li class="day" v-for="(day,key) in days" :key="key">
                            <a href="#" @click="getDayContent(keyMontth + '-' + day)">{{day}}</a>
                        </li>
                    </ul>

                </li>
            </ul>
        </div>
        <div class="">
            <div class="t-left" v-for="day in day_content">
                <span><b>{{day.authorPic}} </b></span> : <span>{{day.authorPic}}</span>
                <div v-html="day.explain"></div>
            </div>
        </div>
    </div>
</template>
<script>
    const appF = firebase.initializeApp(config);
    const dbF = appF.database();


    export default{
        name: 'MainAppNe',
        props:{
        },
        data(){
            return {
                months : {
                    '2018-08' : ['25','26','27'],
                    '2018-09' : ['01','02','03']
                },
                day_content : {

                },
                is_show : false
            }
        },
        methods : {
            getDayContent(day){
                console.log(day)
                dbF.ref('posts').orderByChild('create_at').equalTo(day).once('value').then((data)=>{
                    let arrDay = [];
                    data.forEach((child)=>{
                        arrDay.push(child.val());
                    })
                    console.log(arrDay)
                    this.day_content = arrDay;
                });
                console.log(this.day_content)
            },
            isShow(){
                this.is_show = !this.is_show;
            }
        }
    }
</script>
<style lang="css">
    ul{
        text-align: left;
        list-style: none;
        padding: 0px;
    }
    input[type='text'], textarea{
        height: 22px;
        border: 1px solid #ccc!important;
        padding: 8px;
        margin-bottom: 10px;
    }
    a{
        text-decoration: none;
        display: block;
    }
    .d-in{
        display: inline-block;
    }
    .btn{
        padding: 15px;
    }
    .t-right{
        text-align: right;
    }
    .t-left{
        text-align: left;
    }
    .day{
        padding: 5px 0 5px 20px;
        background-color: #777;
        opacity: 0.8;
        border-bottom: 1px;
    }
    .w-100p{
        width: 100px;
    }
    .w-30{
        width: 15%;
    }
    .w-90{
        width: 90%;
    }
    .w-50{
        width: 50%;
    }
    .w-45{
        width: 45%;
    }
    .w-40{
        width: 40%;
    }
    .collapsible {
      background-color: #777;
      color: white;
      padding: 12px;
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
    .d-flex{
        display: flex;
        flex-wrap: wrap;
    }

</style>
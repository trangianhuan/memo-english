<template>
    <div class="d-flex">
        <div v-show="is_show" class="w-80 t-left d-flex">
            <input id="word" class="fl-g-1" type="text" name="" placeholder="WORD" />
            <input id="mean" class="fl-g-1" type="text" name="" placeholder="MEAN" />
            <textarea id="explain" class="w-100 h-100p" rows="5" placeholder="EXPLAIN" type="text" name=""></textarea>
        </div>
        <a class="btn btn-secondary w-100p" v-show="is_show" @click="save()">Add word</a>
        <div class="w-80 header" v-show="!is_show"> <p>memo english</p></div>
        <a class="btn btn-secondary w-100p" v-show="!is_show" @click="isShow()">Show</a>
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
            },
            save(){
                let d = new Date();
                year = d.getFullYear();
                month = d.getMonth();
                date = d.getDate();
                dbF.ref('years').set();
                dbF.ref('years/'+ year + '-' + month + '/')
                this.is_show = !this.is_show;
            }
        },
        mounted(){
            dbF.ref('posts').once('value')
              .then(function(dataSnapshot) {
                console.log(dataSnapshot.val())
                let data = dataSnapshot.val();
                console.log(typeof data)
                for (let item in data) {
                    console.log(item);
                    for (let d in item) {
                        console.log(d);
                    }
                }
                data.forEach((i,e)=>{console.log(i,e)})
              });
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
    .btn {
        display: inline-block;
        font-weight: 400;
        text-align: center;
        white-space: nowrap;
        vertical-align: middle;
        -webkit-user-select: none;
        -moz-user-select: none;
        -ms-user-select: none;
        user-select: none;
        border: 1px solid transparent;
        padding: .375rem .75rem;
        font-size: 1rem;
        line-height: 1.5;
        border-radius: .25rem;
        transition: color .15s ease-in-out,background-color .15s ease-in-out,border-color .15s ease-in-out,box-shadow .15s ease-in-out;
    }
    .btn-secondary {
        color: #fff;
        background-color: #6c757d;
        border-color: #6c757d;
        margin-left: 1px;
    }
    .d-in{
        display: inline-block;
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
    .h-100p{
        height: 100px;
    }
    .w-100p{
        width: 100px;
    }
    .w-30{
        width: 15%;
    }
    .w-80{
        width: 80%;
    }
    .w-90{
        width: 90%;
    }
    .w-100{
        width: 100%;
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
        align-items: flex-start;
    }
    .fl-g-1{
        flex-grow: 1;
    }
    .fl-g-2{
        flex-grow: 2;
    }
    .header{
        background-color: #6c757d;
        border-radius: .25rem;
        border: 1px solid transparent;
    }
    .header p{
        padding: .55rem .75rem;
        color: #fff;
        margin: 0;
    }

</style>
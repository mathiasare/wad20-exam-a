<template>
<div >
    <button  v-on:click="reverseEntries">{{buttonText}}</button>
    <div class="entry" v-for="entry in entries" :key="entry.id">
            <ul>
                <li><h3>{{entry.title}}</h3></li>
                <li>{{entry.date | formatDate}}</li>
                <li><img  :src="entry.image" alt="post-image"></li>
                <li>{{entry.text}}</li>
            </ul>

    </div>
</div>
</template>

<script>
import moment from 'moment'
    export default {
        name: 'Entries',
        data: function () {
            return {
            buttonText: "Newest to oldest",
            
            }},
        props: {
            entries: Array

            

        },
        filters: {
             formatDate: function (value) {
                return moment(value).format('LLLL');
            }


        },
        computed: {
            sortedEntries: function(){
                let newArray = this.entries;
                return newArray.sort((a, b) => (new Date(a.date) < new Date(b.date)) ? 1 : -1);
            }
        },
        methods:{
            reverseEntries: function (){
                let newArray = this.entries;
                if(this.buttonText=="Newest to oldest"){
                    this.buttonText="Oldest to newest";
                    this.entries=newArray.sort((a, b) => (new Date(a.date) < new Date(b.date)) ? 1 : -1)
                }else{
                    this.buttonText="Newest to oldest"
                    this.entries=newArray.sort((a, b) => (new Date(a.date) > new Date(b.date)) ? 1 : -1)
                }
                
                
            }
        }

    }
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
    h3 {
        margin: 40px 0 0;
    }

    ul {
        list-style-type: none;
        padding: 0;
        display: flex;
        flex-direction: column;
    }

    li {
        
        margin: 0 10px;
    }

    a {
        color: #42b983;
    }
</style>

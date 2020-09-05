<template>
<div>
<div class="col-12">
    <div class="row">
        <template v-for="item in list"><!--- Egehana sor neden kırmızı? --->
            <Card v-bind:title= "item.title" v-bind:body= "item.body" v-bind:url= "item.url"/>
        </template>
    </div>
</div>
</div>
</template>

<script>
import Card from '@/components/card.vue'
import Navbar from '@/components/navbar.vue'

export default {
    name: 'Dashboard',
        data() {
            return {
                message: [],
                photos: [],
                list: [],

        }
    },

    components: {
        Card,
    },

    methods:{
        fetchSomeData(){
            fetch('https://jsonplaceholder.typicode.com/posts', {
            method: 'GET'
            })
            .then(response => response.json())
            .then(json => this.message = json)
        },

        fetchSomePhoto(){
            fetch('https://picsum.photos/v2/list', {
            method: 'GET'
            })
            .then(response => response.json())
            .then(json => this.photos = json);
        },

        MergeTwoAPI(){
            this.list = Object.assign({}, this.message);
            for(var i=0;i<30;i++){
                this.list[i]["url"] = this.photos[i]["download_url"] 
            }
        }
    },

    created(){
        this.fetchSomeData();
        this.fetchSomePhoto();

    },
    watch:{
        photos(){
            this.MergeTwoAPI();
        }
    }
}
</script>

<style>
</style>
<template>
<div class="col-12">
    <div class="row">
        <template v-for="item in message"><!--- Egehana sor neden kırmızı? --->
            <Card v-bind:title="item.title" v-bind:body= "item.body"/>
        </template>
    </div>
</div>
</template>

<script>
import Card from '@/components/card.vue'

export default {
    name: 'Dashboard',
        data() {
            return {
                message: [],
                photos: []

        }
    },

    components: {
        Card
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
            .then(json => this.photos = json)
        }
    },

    created(){
        this.fetchSomeData()
        this.fetchSomePhoto()
    }
    
}
</script>

<style>
</style>
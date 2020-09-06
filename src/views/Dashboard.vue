<template>
  <div>
    <div class="col-12">
      <div class="row">
        <template v-for="item in list">
          <Card
            v-bind:title="item.title"
            v-bind:body="item.body"
            v-bind:url="item.url"
            v-bind:key="item.id"
          />
        </template>
      </div>
    </div>
    <div class="btn-group btn-group-toggle" data-toggle="buttons">
      <label class="btn btn-secondary active" v-if="currentPage != 0">
        <input type="radio" @click="UpdateList(-1)" checked> Önceki
      </label>
      <label class="btn btn-secondary">
        <input type="radio"> {{allPages}} tane sayfadan {{currentPage+1}}.sayfa
      </label>
      <label class="btn btn-secondary" v-if="currentPage != allPages-1" >
        <input type="radio" @click="UpdateList(1)"> Sonraki
      </label>
    </div>
  </div>
</template>

<script>
import Card from "@/components/card.vue";
import Navbar from "@/components/navbar.vue";

export default {
  name: "Dashboard",
  data() {
    return {
      message: [],
      photos: [],
      list: [],
      invisibleList: [],

      //pagination
      currentPage: 0,
      pageSize: 8,
      allPages:0,
    };
  },

  components: {
    Card,
  },

  methods: {
    fetchSomeData() {
      fetch("https://jsonplaceholder.typicode.com/posts", {
        method: "GET",
      })
        .then((response) => response.json())
        .then((json) => (this.message = json));
    },

    fetchSomePhoto() {
      fetch("https://picsum.photos/v2/list", {
        method: "GET",
      })
        .then((response) => response.json())
        .then((json) => (this.photos = json));
    },

    MergeTwoAPI() {
      this.list = Object.assign({}, this.message);
      for (var i = 0; i < 30; i++) {
        this.list[i]["url"] = this.photos[i]["download_url"];
      }
      this.invisibleList=Object.assign({}, this.list);
      this.UpdateList(0);
    },

    UpdateList(index) {
      this.list=[];
      this.allPages=Math.floor(this.message.length/this.pageSize);
      if(this.currentPage < this.allPages && this.currentPage >= 0){
        this.currentPage = this.currentPage + index;
      }
      for (var i = 0; i < this.pageSize; i++ ) {
        this.list[i] = this.invisibleList[this.pageSize*this.currentPage+i]; 
      }
    },
    
  },

  created() {
    this.fetchSomeData();
    this.fetchSomePhoto();
  },
  watch: {
    photos() {
      this.MergeTwoAPI();
    },
  },
};
</script>

<style>
.btn-group{
  margin-bottom: 25px;
}
</style>

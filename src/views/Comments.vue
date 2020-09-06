<template>
  <div>
    <div class="col-12">
      <div class="row">
        <template v-for="item in message">
          <comment-card
            v-bind:name="item.name"
            v-bind:email="item.email"
            v-bind:body="item.body"
          />
        </template>
      </div>
    </div>
  </div>
</template>

<script>
import commentCard from "@/components/commentCard.vue";

export default {
  name: "Comments",
  data() {
    return {
      message: [],
    };
  },

  components: {
    commentCard,
  },

  methods: {
    fetchSomeComment() {
      fetch("https://jsonplaceholder.typicode.com/comments", {
        method: "GET",
      })
        .then((response) => response.json())
        .then((json) => (this.message = json));
    },
  },
  created() {
    this.fetchSomeComment();
  },
};
</script>

<style></style>

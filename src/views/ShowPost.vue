<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <div>
      <h3>{{ this.post.title }}</h3>
      <p>{{ this.post.body }}</p>
      <img v-bind:src="this.post.image" style="width:600px;">

    </div>
  </div>
</template>

<style>
</style>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      message: "Welcome to the Show!",
      post: {},
    };
  },
  created: function () {
    this.showPost();
  },
  methods: {
    showPost: function () {
      console.log("show the post...");
      console.log(this.$route.params.id);
      axios.get(`api/posts/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.post = response.data;
      });
    },
  },
};
</script>
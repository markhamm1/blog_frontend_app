<template>
  <div class="home">
    <h1>{{ message }}</h1>
    <!-- <p>{{ this.posts }}</p> -->
    <div v-for="post in posts">
      <hr>
      <h3><a v-bind:href="`/posts/${post.id}`">{{ post.title }}</a></h3>
      <img v-bind:src="post.image" style="width:250px;">
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
      message: "Welcome to the Index",
      posts: [],
    };
  },
  created: function () {
    this.postsIndex();
  },
  methods: {
    postsIndex: function () {
      console.log("showing index");
      axios.get("api/posts").then((response) => {
        console.log(response.data);
        this.posts = response.data;
      });
    },
  },
};
</script>
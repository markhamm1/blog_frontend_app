// assign default input to form
// allow user to change input
// save input

<template>
  <div class="signup">
    <form v-on:submit.prevent="submit()">
      <h1>Edit Post</h1>
      <ul>
        <li class="text-danger" v-for="error in errors">{{ error }}</li>
      </ul>
      <div class="form-group">
        <label>Titel:</label> 
        <input type="text" class="form-control" v-model="post.title">
      </div>
      <div class="form-group">
        <label>Body:</label>
        <input type="text" class="form-control" v-model="post.body">
        <!-- <textarea name="body" form="form-control"></textarea> -->
      </div>
      <div class="form-group">
        <label>Image:</label>
        <input type="text" class="form-control" v-model="post.image">
      </div>
      <input type="submit" class="btn btn-primary" value="Submit">
    </form>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
      errors: [],
    };
  },
  created: function () {
    this.getPost();
  },
  methods: {
    getPost: function () {
      axios.get(`api/posts/${this.$route.params.id}`).then((response) => {
        console.log(response.data);
        this.post = response.data;
      });
    },

    submit: function () {
      var params = {
        title: this.post.title,
        body: this.post.body,
        image: this.post.image,
      };
      console.log(params);
      axios
        .patch(`/api/posts/${this.$route.params.id}`, params)
        .then((response) => {
          this.$router.push("/posts");
        })
        .catch((error) => {
          this.errors = error.response.data.errors;
        });
    },
  },
};
</script>
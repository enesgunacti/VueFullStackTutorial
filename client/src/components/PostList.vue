<template>
  <div class="container">
    <div v-for="post in posts" :key="post._id" class="card my-5">
      <div class="card-content">
        <div class="media">
          <div class="media-content">
            <p class="title is-4">{{ post.title }}</p>
          </div>
        </div>

        <div class="content">
          {{ post.content }}
          <p />
          <strong>Creator: {{ post.creator }}</strong>
        </div>
      </div>
      <div class="card">
        <footer class="card-footer">
          <button
            @click="editPost(post._id)"
            class="card-footer-item button is-warning"
          >
            Edit
          </button>
          <button
            @click="remowePost(post._id)"
            class="card-footer-item button is-danger"
          >
            Delete
          </button>
        </footer>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
import { useRouter } from "vue-router";
import UpdateVue from "../views/Update.vue";
const router = useRouter();
const API_URL = "http://localhost:5000/posts";
export default {
  created() {
    this.getAllPosts();
    this.remowePost();
    this.editPost();
  },
  data() {
    return {
      posts: [],
    };
  },
  methods: {
    getAllPosts() {
      axios.get(API_URL).then((response) => (this.posts = response.data));
    },
    remowePost(_id) {
      axios
        .delete(`http://localhost:5000/posts/${_id}`)
        .then((response) => {}, this.getAllPosts());
    },
    editPost(_id) {},
  },
};
</script>

<style>
</style>
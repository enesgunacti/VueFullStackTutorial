<template>
  <div class="container mt-5">
    <form @submit.prevent="sendNewPost">
      <div class="field">
        <label class="label">Başlık</label>
        <div class="control">
          <input
            v-model="newPost.title"
            class="input"
            type="text"
            placeholder="Başlık"
            required
          />
        </div>
      </div>

      <div class="field">
        <label class="label">İçerik</label>
        <div class="control">
          <textarea
            v-model="newPost.content"
            class="textarea"
            placeholder="..."
            required
          ></textarea>
        </div>
      </div>

      <div class="field">
        <label class="label">Yazar</label>
        <div class="control">
          <input
            v-model="newPost.creator"
            class="input"
            type="text"
            placeholder="Yazar"
            required
          />
        </div>
      </div>

      <div class="field is-grouped">
        <div class="control">
          <button type="submit" class="button is-primary">Submit</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
import { useRouter } from "vue-router";

import axios from "axios";
const API_URL = "http://localhost:5000/posts";
const router = useRouter();
export default {
  data() {
    return {
      inProgress: false,
      errors: [],
      newPost: {
        title: "",
        content: "",
        creator: "",
      },

      sendNewPostResult: null,
    };
  },
  methods: {
    sendNewPost() {
      this.inProgress = true;
      axios
        .post(API_URL, this.newPost)
        .then((response) => (this.sendNewPostResult = response.data))
        .catch((error) => {
          this.errors.push(error);
        })
        .finally(() => (this.inProgress = false));
      this.$router.push("/");
    },
  },
};
</script>

<style>
</style>
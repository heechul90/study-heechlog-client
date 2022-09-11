<script setup lang="ts">
import axios from "axios";
import {ref} from "vue";

const posts = ref([]);

axios.get("/api/posts").then((response) => {
  response.data.data.forEach(function (row:any) {
    posts.value.push(row);
  });
});

</script>

<template>

  <ul>
    <li v-for="post in posts" :key="post.postId">
      <div>
        {{post.postTitle}}
      </div>
      <div>
        {{post.postContent}}
      </div>
    </li>
  </ul>

</template>

<style scoped>

li {
  margin-bottom: 1rem;
}

li:last-child {
  margin-bottom: 0;
}

</style>

<script setup lang="ts">
import {defineProps, onMounted, ref} from "vue";
import axios from "axios";

const props = defineProps({
  postId: {
    type: [Number, String],
    required: true,
  },
});

const post = ref({
  postId: 0,
  postTitle: "",
  postContent: ""
});

onMounted(() => {
  axios
      .get(`/api/posts/${props.postId}`)
      .then((response) => {
        post.value = response.data.data;
      });
});

</script>

<template>
  <h2>{{post.postTitle}}</h2>
  <div>{{post.postContent}}</div>
</template>

<style scoped>

</style>
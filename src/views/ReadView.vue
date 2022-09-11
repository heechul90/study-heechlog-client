<script setup lang="ts">
import {defineProps, onMounted, ref} from "vue";
import axios from "axios";
import router from "@/router";

const props = defineProps({
  postId: {
    type: [Number, String],
    require: true,
  },
});

const post = ref({
  postId: 0,
  postTitle: "",
  postContent: ""
});

const moveToEdit = () => {
  router.push({name: "edit", params: {postId: props.postId}});
};

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

  <el-button type="warning" @click="moveToEdit()">수정</el-button>

</template>

<style scoped>

</style>
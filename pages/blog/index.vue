<template>
  <div>
    <h1 class="mb-10">Blog</h1>
    <nuxt-link
      :to="`/blog/${post.slug}`"
      v-for="(post, keyPost) in list"
      :key="keyPost"
      class="block mb-5 underline"
      >{{ post.title }}</nuxt-link
    >
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      list: []
    };
  },
  asyncData({ params, error }) {
    return axios
      .get(`https://service.mockapi.me/api/sinanyaman/list-posts`)
      .then(({ data }) => {
        return { list: data };
      })
      .catch(() => {
        error({ statusCode: 404, message: "Post not found" });
      });
  }
};
</script>

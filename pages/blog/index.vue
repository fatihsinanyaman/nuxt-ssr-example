<template>
  <div>
    <h1 class="mb-10">Blog</h1>
    <hr class="my-6">
    <h1 class="font-bold ml-6 text-3xl" v-if="$fetchState.pending">yukleniyor</h1>
    <h1 class="font-bold ml-6 text-3xl" v-else>{{ data.config.title }}</h1>
    <hr class="my-6">
    <nuxt-link
      :to="`/blog/${post.id}`"
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
      list: [],
      data: {}
    };
  },
   async fetch() {
      this.data = await fetch(
        'https://run.mocky.io/v3/758cec98-9442-4e42-9c8e-e43b443c9019?mocky-delay=5000ms'
      ).then(res => res.json())
    },
  asyncData({ params, error }) {
    return axios
      .get(`https://jsonplaceholder.typicode.com/posts`)
      .then(({ data }) => {
        return { list: data };
      })
      .catch(() => {
        error({ statusCode: 404, message: "Post not found" });
      });
  }
};
</script>

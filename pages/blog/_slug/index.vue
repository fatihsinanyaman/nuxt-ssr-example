<template>
  <div>
    <h2>{{ title }}</h2>
    <p>{{ body }}</p>
  </div>
</template>
<script>
import axios from "axios";
export default {
  data() {
    return {
      title: "Not set yet"
    };
  },
  asyncData({ params, error }) {
    return axios
      .get(`https://jsonplaceholder.typicode.com/posts/${params.slug}`)
      .then(res => {
        return { title: res.data.title, body: res.data.body };
      })
      .catch(() => {
        error({ statusCode: 404, message: "Post not found" });
      });
  }
};
</script>

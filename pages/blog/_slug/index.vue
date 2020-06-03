<template>
  <div>
    <h2>Slug</h2>
    <p>{{ title }}</p>
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
      .get(`https://service.mockapi.me/api/sinanyaman/${params.slug}`)
      .then(res => {
        return { title: res.data.data };
      })
      .catch(() => {
        error({ statusCode: 404, message: "Post not found" });
      });
  }
};
</script>

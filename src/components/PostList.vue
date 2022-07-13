<template>
  <div class="post-container">
    <h3>Posts list</h3>
    <post-item v-for="post in posts" :post="post" :key="post.id"/>
  </div>
</template>

<script>
import PostItem from '@/components/PostItem';
export default {
  components: {PostItem},
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
}
</script>

<style scoped>
.post-container {
  width: 70%;
}
</style>

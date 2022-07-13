<template>
  <div class="post-container" v-if="posts.length > 0">
    <h3>Posts list</h3>
    <post-item
      v-for="post in posts"
      :post="post"
      :key="post.id"
      @remove="$emit('remove', post)"
    />
  </div>
  <div v-else>
    <h3 style="color: red">No posts found</h3>
  </div>
</template>

<script>
import PostItem from "@/components/PostItem";
export default {
  components: { PostItem },
  props: {
    posts: {
      type: Array,
      required: true,
    },
  },
};
</script>

<style scoped>
.post-container {
  width: 70%;
}
</style>

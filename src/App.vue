<template>
  <div class="app">
    <post-form @create="createPost" />
    <post-list :posts="posts" />
  </div>
</template>

<script>
import PostList from "@/components/PostList";
import PostForm from "@/components/PostForm";

export default {
  components: {
    PostList,
    PostForm,
  },
  data() {
    return {
      posts: [
        { id: 1, title: "About Javascript 1", body: "A lot of text" },
        { id: 2, title: "About Javascript 2", body: "A lot of text" },
        { id: 3, title: "About Javascript 3", body: "A lot of text" },
        { id: 4, title: "About Javascript 4", body: "A lot of text" },
      ],
      title: "",
      body: "",
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
    },
  },
};
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  width: 100%;
  height: 100vh;
}
</style>

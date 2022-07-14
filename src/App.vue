<template>
  <div class="app">
    <h1 style="margin-bottom: 25px">Page with posts</h1>
    <my-button @click="showDialog">Add post</my-button>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>
    <post-list :posts="posts" @remove="removePost" />
  </div>
</template>

<script>
import PostList from "@/components/PostList";
import PostForm from "@/components/PostForm";
import MyDialog from "@/components/ui/MyDialog";
import MyButton from "@/components/ui/MyButton";

export default {
  components: {
    MyButton,
    MyDialog,
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
      dialogVisible: false,
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },
    showDialog() {
      this.dialogVisible = true;
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

<template>
  <div class="app">
    <h1 style="margin-bottom: 25px">Page with posts</h1>

    <my-input
      v-model="searchQuery"
      style="max-width: 70%"
      placeholder="Type query"
    />

    <div class="app-buttons">
      <my-button @click="showDialog">Add post</my-button>
      <my-select v-model="selectedSort" :options="sortOptions" />
    </div>

    <input type="text" v-model.trim="modificationValue" />

    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>

    <post-list
      :posts="sortedAndSearchedPosts"
      @remove="removePost"
      v-if="!isPostsLoading"
    />

    <div v-else>Loading...</div>
  </div>
</template>

<script>
import axios from "axios";
import PostList from "@/components/PostList";
import PostForm from "@/components/PostForm";
import MyDialog from "@/components/ui/MyDialog";
import MyButton from "@/components/ui/MyButton";
import MySelect from "@/components/ui/MySelect";
import MyInput from "@/components/ui/MyInput";

export default {
  components: {
    MySelect,
    MyButton,
    MyDialog,
    PostList,
    PostForm,
    MyInput,
  },

  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: true,
      modificationValue: "",
      selectedSort: "title",
      searchQuery: "",

      sortOptions: [
        { value: "title", name: "Title" },
        { value: "body", name: "Body" },
      ],
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
    async fetchPosts() {
      try {
        this.isPostsLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts?_limit=10"
        );
        this.posts = response.data;
        this.isPostsLoading = false;
      } catch (error) {
        console.log(error);
      } finally {
        this.isPostsLoading = false;
      }
    },
  },
  mounted() {
    this.fetchPosts();
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((post1, post2) => {
        return post1[this.selectedSort]?.localeCompare(
          post2[this.selectedSort]
        );
      });
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter((post) => {
        return post[this.selectedSort]
          .toLowerCase()
          .includes(this.searchQuery.toLowerCase());
      });
    },
  },
  watch: {
    // selectedSort(newValue) {
    //   this.posts.sort((post1, post2) => {
    //     return post1[newValue]?.localeCompare(post2[newValue]);
    //   });
    // },
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

.app-buttons {
  width: 70%;
  display: flex;
  justify-content: space-between;
  margin-bottom: 25px;
}
</style>

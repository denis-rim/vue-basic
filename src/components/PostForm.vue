<template>
  <form @submit.prevent>
    <h4>Create Post</h4>
    <my-input v-model="post.title" placeholder="Title" />
    <my-input v-model="post.body" placeholder="Description" />
    <div class="button-wrapper">
      <my-button @click="createPost"> Submit </my-button>
    </div>
  </form>
</template>

<script>
export default {
  data() {
    return {
      post: {
        title: "",
        body: "",
      },
    };
  },
  methods: {
    createPost() {
      if (!this.post.title || !this.post.body) {
        return;
      }

      this.post.id = Date.now();
      this.$emit("create", this.post);
      this.post = {
        title: "",
        body: "",
      };
    },
  },
};
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
  width: 70%;
}

.button-wrapper {
  align-self: flex-end;
}
</style>

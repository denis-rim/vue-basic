<template>
  <div class="post">
    <div>
      <div class="">
        Name: <strong>{{ post.title }}</strong>
      </div>
      <div class="">
        Description: <strong>{{ post.body }}</strong>
      </div>
    </div>
    <div>
      <my-button @click="$emit('remove', post)" class="post-delete"
        >Удоли!</my-button
      >
    </div>
  </div>
</template>

<script>
export default {
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style scoped>
.post {
  display: flex;
  justify-content: space-between;
  align-items: center;
  border: 2px solid #ccc;
  padding: 10px;
  margin: 10px auto;
}

.post-delete {
  background-color: red !important;
  color: white !important;
}
</style>

<template>
  <div class="dialog" v-if="show" @click="hideDialog">
    <div class="dialog-content" @click.stop>
      <slot></slot>
    </div>
  </div>
</template>

<script>
export default {
  name: "my-dialog",
  props: {
    show: {
      type: Boolean,
      required: true,
    },
  },
  methods: {
    hideDialog() {
      this.$emit("update:show", false);
    },
  },
};
</script>

<style scoped>
.dialog {
  display: flex;
  flex-direction: column;
  position: fixed;
  top: 0;
  bottom: 0;
  left: 0;
  right: 0;
  background-color: rgba(0, 0, 0, 0.5);
  z-index: 100;
}

.dialog-content {
  justify-content: center;
  align-items: center;
  background: white;
  margin: auto;
  border-radius: 15px;
  min-height: 200px;
  min-width: 500px;
}
</style>

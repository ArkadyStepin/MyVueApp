<template>
  <dvi class="dialog" v-if="show" @click.stop="hideDialog">
    <div @click.stop class="dialogContent">
      <slot></slot>
    </div>
  </dvi>
</template>

<script>
export default {
  name: "my-dialog",
  props: {
    show: {
      type: Boolean,
      default: false,
    },
  },
  methods: {
    hideDialog() {
      this.$emit("update:show", false);
    },
  },
};
</script>

<style>
.dialog {
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
  background: rgba(0, 0, 0, 0.5);
  position: fixed;
  display: flex;
}
.dialogContent {
  margin: auto;
  padding: 20px;
  background: whitesmoke;
  border-radius: 12px;
  min-height: 50px;
  min-width: 300xp;
}
</style>

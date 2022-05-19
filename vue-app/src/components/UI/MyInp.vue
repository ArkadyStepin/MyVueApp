<template>
  <input :value="modelValue" @input="updateInp" type="text" class="inp" />
</template>

<script>
export default {
  name: "my-inp",
  props: {
    modelValue: [String, Number],
  },
  methods: {
    updateInp(event) {
      this.$emit("update:modelValue", event.target.value);
    },
  },
};
</script>

<style>
.inp {
  width: 100%;
  border: 2px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}
</style>

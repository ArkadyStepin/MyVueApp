<template>
  <div class="post">
    <div>
      <div><strong> Название: </strong> {{ post.title }}</div>
      <div><strong> Описание: </strong> {{ post.body }}</div>
    </div>
    <div class="postButtons">
      <my-btn>Delete</my-btn>
    </div>
  </div>
</template>

<script>
import MyBtn from "./UI/MyBtn.vue";
export default {
  components: {
    MyBtn,
  },
  props: {
    post: {
      type: Object,
      required: true,
    },
  },
};
</script>

<style>
.post {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px;
  border: 3px solid teal;
  margin-top: 15px;
}
</style>

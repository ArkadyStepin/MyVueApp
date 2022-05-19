<template>
  <div class="post">
    <div>
      <div>{{ post.id }}</div>
      <div><strong> Название: </strong> {{ post.title }}</div>
      <div><strong> Описание: </strong> {{ post.body }}</div>
    </div>
    <div class="postButtons">
      <my-btn @click="$router.push(`/posts/${post.id}`)"> Open</my-btn>
    </div>

    <div class="postButtons">
      <my-btn @click="$emit('remove', post)"> Delete</my-btn>
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

<style>
.post {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 15px;
  border: 3px solid teal;
  margin-top: 15px;
}
.postButtons {
  margin-left: 5px;
}
</style>

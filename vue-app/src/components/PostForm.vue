<template>
  <form @submit.prevent>
    <h4>Create post form</h4>
    <input
      v-model="post.title"
      class="inp"
      type="text"
      placeholder="post title"
    />
    <input
      v-model="post.body"
      class="inp"
      type="text"
      placeholder="post body"
    />
    <my-btn class="createBtn" @click="createPost">Create</my-btn>
  </form>
</template>

<script>
import MyBtn from "./UI/MyBtn.vue";
export default {
  components: {
    MyBtn,
  },
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
      this.id = Date.now();
      this.$emit("create", this.post);
      this.post = {
        title: "",
        body: "",
      };
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
.createBtn {
  align-self: flex-end;
  margin: 15px 16px 0px 0px;
}
form {
  display: flex;
  flex-direction: column;
}
</style>

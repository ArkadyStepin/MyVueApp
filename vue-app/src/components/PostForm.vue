<template>
  <form @submit.prevent>
    <h4>Create post form</h4>
    <my-inp v-model="post.title" placeholder="post title" />
    <my-inp v-model="post.body" placeholder="post body" />
    <my-btn class="createBtn" @click="createPost">Create</my-btn>
  </form>
</template>

<script>
import MyInp from "./UI/MyInp.vue";
export default {
  components: { MyInp },
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
.createBtn {
  align-self: flex-end;
  margin: 15px 16px 0px 0px;
}
form {
  display: flex;
  flex-direction: column;
}
</style>

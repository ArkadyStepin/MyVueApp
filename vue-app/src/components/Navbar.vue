<template>
  <div class="navbar">
    <my-btn @click="$router.push('/')" class="one-navbar-btn">Vue 3</my-btn>
    <div class="navbar-btn">
      <my-btn @click="$router.push('/posts')" class="one-navbar-btn"
        >Posts</my-btn
      >
      <my-btn @click="$router.push('/about')" class="one-navbar-btn"
        >about app</my-btn
      >
    </div>
  </div>
</template>

<script>
export default {};
</script>

<style scoped>
.navbar {
  height: 50px;
  background-color: rgba(103, 114, 8, 0.774);
  box-shadow: 2px 2px 4px greenyellow;
  display: flex;
  align-items: center;
  padding: 0px 15px;
}
.navbar-btn {
  margin-left: auto;
}
.one-navbar-btn {
  border: none !important;
  font: 25px bold !important;
  cursor: pointer;
}
</style>

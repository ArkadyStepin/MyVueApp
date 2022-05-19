<template>
  <div >
    <h1>Page with posts</h1>
    <my-inp v-model="searchQuery" placeholder="search..." />

    <div class="appBtns">
      <my-btn @click="showDialog"> Create post </my-btn>
      <my-select v-model="selectedSort" :options="sortOptions"> </my-select>
    </div>
    <my-dialog v-model:show="dialogVisible">
      <post-form @create="createPost" />
    </my-dialog>
    <post-list
      :posts="sortedAndSearchedPost"
      @remove="removePost"
      v-if="!isPostLoading"
    />
    <div v-else>loading in process...</div>
    <div ref="observer" class="observer"></div>
  </div>
</template>

<script>
import PostForm from "@/components/PostForm";
import PostList from "@/components/PostList";
import axios from "axios";

export default {
  components: {
    PostForm,
    PostList,
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostLoading: false,
      selectedSort: "",
      sortOptions: [
        { value: "title", name: "by name" },
        { value: "body", name: "by content" },
      ],
      searchQuery: "",
      page: 1,
      limitPage: 10,
      totalPages: 0,
    };
  },
  methods: {
    createPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },

    removePost(post) {
      this.posts = this.posts.filter((p) => p.id !== post.id);
    },

    showDialog() {
      this.dialogVisible = true;
    },

    async fetchPosts() {
      try {
        this.isPostLoading = true;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",
          {
            params: {
              _page: this.page,
              _limit: this.limitPage,
            },
          }
        );
        this.totalPages = Math.ceil(
          response.headers["x-total-count"] / this.limitPage
        );
        this.posts = response.data;
      } catch (error) {
        alert("erOOOR");
      } finally {
        this.isPostLoading = false;
      }
    },

    async loadMorePosts() {
      try {
        this.page += 1;
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/posts",
          {
            params: {
              _page: this.page,
              _limit: this.limitPage,
            },
          }
        );
        this.totalPages = Math.ceil(
          response.headers["x-total-count"] / this.limitPage
        );
        this.posts = [...this.posts, ...response.data];
      } catch (error) {
        alert("Ошибка");
      }
    },
  },

  mounted() {
    this.fetchPosts();
    const options = {
      rootMargin: "0px",
      threshold: 1.0,
    };

    const callback = (entries, observer) => {
      if (entries[0].isIntersecting && this.page < this.totalPages) {
        this.loadMorePosts();
      }
    };

    const observer = new IntersectionObserver(callback, options);
    observer.observe(this.$refs.observer);
  },
  computed: {
    sortedPosts() {
      return [...this.posts].sort((a, b) => {
        return a[this.selectedSort]?.localeCompare(b[this.selectedSort]);
      });
    },

    sortedAndSearchedPost() {
      return this.sortedPosts.filter((post) =>
        post.title.toLowerCase().includes(this.searchQuery.toLowerCase())
      );
    },
  },
};
</script>

<style>

.appBtns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
.observer {
  height: 10px;
  }
</style>


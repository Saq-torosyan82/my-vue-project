<template>
<div class="app">
  <h1>Posts page</h1>
  <my-button @click="showDialog" style="margin: 15px 0">Create Post</my-button>
  <my-dialog v-model:show="dialogVisible">
    <post-form @createPost="addPost" />
  </my-dialog>  
  <post-list v-if="!isPostsLoading" :posts="posts" @remove="removePost" />
  <div v-else>Loading posts ...</div>
</div>
</template>

<script>
import PostList from "@/components/PostList";
import PostForm from "@/components/PostForm";
import axios from "axios";

export default {
  components: {
    PostList,
    PostForm,
  },
  data() {
    return {
      posts: [],
      dialogVisible: false,
      isPostsLoading: false,
    }
  },
  methods: {
    addPost(post) {
      this.posts.push(post);
      this.dialogVisible = false;
    },
    removePost(post) {
      this.posts = this.posts.filter(p => p.id !== post.id);
    },
    showDialog() {
      this.dialogVisible = true;
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true
        const response = await axios.get("https://jsonplaceholder.typicode.com/posts?_limit=10");
        this.posts = response.data;        
      } catch (err) {
        alert("Error")
      } finally {
        this.isPostsLoading = false;
      }
    }
  },
  mounted() {
    this.fetchPosts();
  }
}
</script>

<style>
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

.app {
  padding: 20px;
}
</style>
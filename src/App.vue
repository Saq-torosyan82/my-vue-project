<template>
<div class="app">
  <h1>Posts page</h1>

  <div class="app__btns">
    <my-button @click="showDialog">Create Post</my-button>

    <my-select v-model="selectedSort" :options="sortOptions" />
  </div>
  
  <my-dialog v-model:show="dialogVisible">
    <post-form @createPost="addPost" />
  </my-dialog>  
  <post-list v-if="!isPostsLoading" :posts="sortedPosts" @remove="removePost" />
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
      selectedSort: '',
      sortOptions: [
        {value: 'title', name: 'Sort by title'},
        {value: 'body', name: 'Sort by body'}
      ]
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
  },
  computed: {
    sortedPosts() {
      return [...this.posts.sort((post1, post2) => post1[this.selectedSort]?.localeCompare(post2[this.selectedSort]))]
    }
  },
  watch: {
    /*selectedSort(newVal) {
      this.posts.sort((post1, post2) => post1[newVal]?.localeCompare(post2[newVal]))
    }*/
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

.app__btns {
  margin: 15px 0;
  display: flex;
  justify-content: space-between;
}
</style>
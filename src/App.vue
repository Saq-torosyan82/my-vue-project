<template>
<div class="app">
  <h1>Posts page</h1>
  <my-input v-model="searchTerm" placeholder="Search ... ">

  </my-input>
  <div class="app__btns">
    <my-button @click="showDialog">Create Post</my-button>

    <my-select v-model="selectedSort" :options="sortOptions" />
  </div>
  
  <my-dialog v-model:show="dialogVisible">
    <post-form @createPost="addPost" />
  </my-dialog>  
  <post-list v-if="!isPostsLoading" :posts="sortedAndSearchedPosts" @remove="removePost" />
  <div v-else>Loading posts ...</div>
  <div class="page__wrapper">
    <div
     v-for="pageNum in totalPages"
     :key="pageNum"
     class="page"
     :class="{current_page: pageNum === page}"
     @click="changePage(pageNum)"
    >
      {{ pageNum }}
    </div>
  </div>
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
      searchTerm: '',
      page: 1,
      limit: 10,
      totalPages: 0,
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
    changePage(pageNum) {
      this.page = pageNum;
      // this.fetchPosts();
    },
    async fetchPosts() {
      try {
        this.isPostsLoading = true
        const response = await axios.get("https://jsonplaceholder.typicode.com/posts", {
          params: {
            _page: this.page,
            _limit: this.limit
          }
        });
        this.totalPages = Math.ceil(response.headers['x-total-count'] / this.limit);
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
    },
    sortedAndSearchedPosts() {
      return this.sortedPosts.filter(post => post.title.toLowerCase().includes(this.searchTerm.toLowerCase()))
    }
  },
  watch: {
    page() {
      this.fetchPosts();
    }
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

.page__wrapper {
  display: flex;
  margin-top: 15px;
}

.page {
  border: 1px solid black;
  padding: 10px;
  cursor: pointer;
  margin-left: 10px;
}

.current_page {
  border: 2px solid teal;
}
</style>
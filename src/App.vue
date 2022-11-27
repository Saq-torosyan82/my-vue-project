<template>
<div class="app">
  <h1>Posts page</h1>
  <my-button @click="showDialog" style="margin: 15px 0">Create Post</my-button>
  <my-dialog v-model:show="dialogVisible">
    <post-form @createPost="addPost" />
  </my-dialog>  
  <post-list :posts="posts" @remove="removePost" />
</div>
</template>

<script>
import PostList from "@/components/PostList";
import PostForm from "@/components/PostForm";

export default {
  components: {
    PostList,
    PostForm,
  },
  data() {
    return {
      posts: [
        {id: 1, title: 'Post 1', body: 'This is post 1'},
        {id: 2, title: 'Post 2', body: 'This is post 2'},
        {id: 3, title: 'Post 3', body: 'This is post 3'},
        {id: 4, title: 'Post 4', body: 'This is post 4'},
        {id: 5, title: 'Post 5', body: 'This is post 5'},
        {id: 6, title: 'Post 6', body: 'This is post 6'},
      ],
      dialogVisible: false,
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
</style>
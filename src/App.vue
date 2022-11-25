<template>
<div class="app">
  <post-form @createPost="addPost" />
  <post-list :posts="posts" />
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
    }
  },
  methods: {
    addPost(post) {
      this.posts.push(post);
    },
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
<template>
<div class="app">
  <div>
    <form @submit.prevent>
      <h4>Create Post</h4>
      <input v-bind:value="title" @input="title = $event.target.value" class="input" type="text" placeholder="Title">
      <input v-bind:value="body" @input="body = $event.target.value" class="input" type="text" placeholder="Body">
      <button class="btn" @click="createPost">Create</button>
    </form>
  </div>
  <div class="post" v-for="post in posts">
    <div><strong>Title:</strong> {{ post.title }}</div>
    <div><strong>Body:</strong> {{ post.body }}</div>
  </div>
</div>
</template>

<script>
export default {
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
      title: '',
      body: '',
    }
  },
  methods: {
    createPost(event) {
      event.stopPropagation()

      const newPost = {
        id: Date.now(),
        title: this.title,
        body: this.body
      }

      this.posts.push(newPost);
      this.resetForm()
    },
    resetForm() {
      this.title = '';
      this.body = '';
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

form {
  display: flex;
  flex-direction: column;
}

.post {
  padding: 15px;
  border: 2px solid teal;
  margin-top: 15px;
}

.input {
  width: 100%;
  border: 1px solid teal;
  padding: 10px 15px;
  margin-top: 15px;
}

.btn {
  margin-top: 15px;
  align-self: flex-end;
  padding: 10px 15px;
  background: none;
  border: 1px solid teal;
  cursor: pointer;
  color: teal;
}
</style>
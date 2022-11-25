<template>
  <div>
    <form @submit.prevent>
      <h4>Create Post</h4>
      <input v-model="post.title" class="input" type="text" placeholder="Title">
      <input v-model="post.body" class="input" type="text" placeholder="Body">
      <button class="btn" @click="createPost">Create</button>
    </form>
  </div>
</template>

<script>
export default {
  name: "PostForm",
  data() {
    return {
      post: {
        title: '',
        body: ''
      }
    }
  },
  methods: {
    createPost() {
      this.post.id = Date.now();
      this.$emit('createPost', this.post)
      this.resetForm()
    },
    resetForm() {
      this.post = {
        title: '',
        body: ''
      }
    }
  }
}
</script>

<style scoped>
form {
  display: flex;
  flex-direction: column;
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
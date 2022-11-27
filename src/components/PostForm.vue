<template>
  <div>
    <form @submit.prevent>
      <h4>Create Post</h4>
      <my-input
        v-model="post.title"
        placeholder="Title"
      />
      <my-input
        v-model="post.body"
        placeholder="Body"
      />
      <my-button
        style="align-self: flex-end; margin-top: 15px;"
        @click="createPost"
      >
        Create
      </my-button>
    </form>
  </div>
</template>

<script>
export default {
  name: "PostForm",
  components: {
  },
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
</style>
<template>
  <div v-if="posts.length > 0">
    <h3>Posts List</h3>
    <TransitionGroup name="posts-list">
      <post-item v-for="post in posts" :post="post" :key="post.id" @remove="$emit('remove', post)" />
    </TransitionGroup>    
  </div>
  <h3 v-else style="color: red">There are no posts</h3>

</template>

<script>
import PostItem from "@/components/PostItem";

export default {
  name: "PostList",
  components: {
    PostItem
  },
  props: {
    posts: {
      type: Array,
      required: true,
    }
  }
}
</script>

<style scoped>
.posts-list-enter-active,
.posts-list-leave-active {
  transition: all 0.5s ease;
}
.posts-list-enter-from,
.posts-list-leave-to {
  opacity: 0;
  transform: translateX(30px);
}
</style>
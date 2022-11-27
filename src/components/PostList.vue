<template>
  <div>
    <h3>Posts List</h3>
    <post-item v-for="post in posts" :post="post" :key="post.id" @remove="$emit('remove', post)" />
  </div>


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

</style>
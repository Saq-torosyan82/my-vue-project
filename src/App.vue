<template>
<div>
  <div>Likes count:  <strong>{{ likes }}</strong></div>
  <div>Dislikes count:  <strong>{{ dislikes }}</strong></div>
</div>
</template>

<script>
export default {
  data() {
    return {
      likes: 0,
      dislikes: 0,
    }
  }
}
</script>

<style scoped>

</style>
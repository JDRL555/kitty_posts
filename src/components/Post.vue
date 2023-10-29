<script setup>
  const { 
    post, increment, displayPost 
  } = defineProps({ post: Object, increment: Function, displayPost: Boolean })
</script>

<template>
  <div :class="displayPost" class="post">
    <div class="options">
      <p class="point">⚪</p>
      <p class="point">⚪</p>
      <p class="point">⚪</p>
    </div>
    <img :src=post.src :alt=post.title >
    <div class="post_body">
      <div class="post_info">
        <h3>{{ post.title }}</h3>
        <p>{{ post.description }}</p>
      </div>
      <div class="post_footer">
        <button @click="increment(post)">❤</button>
        <p>Likes: {{ post.likes }}</p>
      </div>
    </div>
  </div>
</template>
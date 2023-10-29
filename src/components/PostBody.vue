<script setup>
  import { inject } from 'vue'
  const post = inject("post")
  const increment = inject("increment")
</script>

<template >
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
</template>
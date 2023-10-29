<script setup>
  import { provide }  from 'vue'

  import PostOptions  from './PostOptions.vue'
  import PostBody     from './PostBody.vue'
  
  const { 
    post, increment, displayPost 
  } = defineProps({ post: Object, increment: Function, displayPost: Boolean })

  provide("post", post)
  provide("increment", increment)
</script>

<template>
  <div :class="displayPost" class="post">
    <PostOptions />
    <img :src=post.src :alt=post.title >
    <PostBody />
  </div>
</template>
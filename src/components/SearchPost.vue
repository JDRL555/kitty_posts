<script setup>
  import {ref} from 'vue'
  let { 
    found, 
    foundPosts,
    posts,
    setFound,
    setPosts,
    addPost,
    clearPosts
  } = defineProps(
    { 
      posts: Object, 
      foundPosts: Object,
      found: Boolean, 
      setFound: Function, 
      setPosts: Function, 
      addPost: Function, 
      clearPosts: Function, 
    }
  )

  let onInput = e => {
  const valueLower  = e.target.value.toLowerCase()
  clearPosts()

  posts.forEach(post => {
    const titleLower  = post.title.toLowerCase()
    if(titleLower.includes(valueLower)) {
      addPost(post)
      setFound(true)   
    } 
  })
  
  if(!valueLower) {
    setFound(true)
    setPosts(ref([...posts]))
  }   
  if(!foundPosts.length) setFound(false)
}
</script>

<template>
  <section class="search">
    <input 
      type="text" 
      id="search" 
      placeholder="Search a post by it title!"
      @input="onInput"
    >
  </section>
</template>

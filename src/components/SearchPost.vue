<script setup>
  import {ref} from 'vue'
  let { 
    found, 
    foundPosts,
    posts,
    setFound,
  } = defineProps(
    { 
      posts: Object, 
      foundPosts: Object,
      found: Boolean, 
      setFound: Function 
    }
  )

  const setPosts = (foundPosts, newPosts) => {
    foundPosts = newPosts
  }

  const addPost = (foundPosts, newPost) => {
    foundPosts.push(newPost)
  }

  const clearPosts = foundPosts => {
    foundPosts.length = 0
  }

  let onInput = e => {
  const valueLower  = e.target.value.toLowerCase()
  clearPosts(foundPosts)

  posts.forEach(post => {
    const titleLower  = post.title.toLowerCase()
    if(titleLower.includes(valueLower)) {
      addPost(foundPosts, post)
      setFound(true)   
    } 
  })
  
  if(!valueLower) {
    setFound(true)
    setPosts(foundPosts, ref([...posts]))
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

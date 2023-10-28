<script setup>
import { computed }   from '@vue/reactivity'
import { ref }        from 'vue'
import posts          from './utils/posts.json'

posts.forEach(post => post.likes = ref(0))

let foundPosts = ref([...posts])

let title = "Kitty Posts"

let found = ref(true)

const displayPost = computed(() => !found.value ? "invisible" : "visible")

let increment = post => post.likes.value++

let onInput = e => {
  const valueLower  = e.target.value.toLowerCase()
  // const foundPosts = posts.filter(post => post.title.toLowerCase().includes(valueLower))
  foundPosts.value.splice(0, foundPosts.value.length)

  posts.forEach(post => {
    const titleLower  = post.title.toLowerCase()
    if(titleLower.includes(valueLower)) {
      foundPosts.value.push(post)
      found.value = true   
    } 
  })
  
  if(!valueLower) {
    found.value = true
    foundPosts = ref([...posts])
  }   
  if(!foundPosts.value.length) found.value = false
}

</script>

<template>
  <main>
    <h1>{{ title }}</h1>
    <section class="search">
      <input 
        type="text" 
        id="search" 
        placeholder="Search a post by it title!"
        @input="onInput"
      >
    </section>
    <section class="posts">
      <h2 v-if="!found">Post not Found:(</h2>
      <div v-for="post in foundPosts" :class="displayPost" class="post">
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
    </section>
    <button 
      class="create" 
      type="submit"
    >
      Create post
    </button>
  </main>
</template>
<script setup>
import { computed }   from '@vue/reactivity'
import { ref }        from 'vue'

const title = "Kitty Posts"

const post_title        = "Gato reflexivo"
const post_description  = "Ta pensativo de la vida"

const img = "https://images.unsplash.com/photo-1595433707802-6b2626ef1c91?auto=format&fit=crop&q=80&w=1000&ixlib=rb-4.0.3&ixid=M3wxMjA3fDB8MHxleHBsb3JlLWZlZWR8Mnx8fGVufDB8fHx8fA%3D%3D"

let counter = ref(0)
let found   = ref(true)

const displayPost   = computed(() => !found.value ? "invisible" : "visible")

let increment = () => counter.value++

let onInput = e => {
  const valueLower  = e.target.value.toLowerCase()
  const titleLower  = post_title.toLowerCase()
  
  titleLower.includes(valueLower) 
  ? found.value = true 
  : found.value = false

  if(!valueLower) found.value = true 
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
      <div :class="displayPost" class="post">
        <div class="actions">
          <p class="action">⚪</p>
          <p class="action">⚪</p>
          <p class="action">⚪</p>
        </div>
        <img :src=img :alt=img >
        <h3>{{ post_title }}</h3>
        <p>{{ post_description }}</p>
        <div class="likes">
          <button @click="increment">❤</button>
          <p>Likes: {{ counter }}</p>
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
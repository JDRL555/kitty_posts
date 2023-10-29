<script setup>
  import { computed }   from '@vue/reactivity'
  import { ref, watch } from 'vue'

  import SearchPost     from './components/SearchPost.vue'
  import Posts          from './components/Posts.vue'
  import Post           from './components/Post.vue'

  import posts          from './utils/posts.json'

  posts.forEach(post => post.likes = ref(0))

  let foundPosts = ref([...posts])

  let found = ref(true)

  let setFound = newValue => found.value = newValue

  const displayPost = computed(() => !found.value ? "invisible" : "visible")

  let increment = post => post.likes++
</script>

<template>
  <main>
    <h1>Kitty Posts</h1>

    <SearchPost 
      :posts=posts 
      :found=found 
      :foundPosts=foundPosts
      :setFound=setFound
    />

    <Posts :found=found>
      <template v-slot:title>
        <h2 v-if="!found">Post not Found:(</h2>
      </template>
      <template v-slot:posts>
        <div v-for="post in foundPosts" :class="displayPost" class="post">
          <Post 
            :post=post 
            :increment=increment 
          />
        </div>
      </template>
    </Posts>

    <button 
      class="create" 
      type="submit"
    >
      Create post
    </button>
  
  </main>
</template>
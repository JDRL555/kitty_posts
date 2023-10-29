<script setup>
  const { found } = defineProps({ found: Boolean })
</script>

<template>
  <section class="posts">
    <slot name="title"></slot>
    <slot name="posts"></slot>
  </section>
</template>
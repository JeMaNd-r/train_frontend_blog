<script setup lang="ts">
const blog_posts = ref(null)

async function fetchPosts() {
  blog_posts.value = null
  const resp = await fetch(
    "https://jsonplaceholder.typicode.com/posts"
  )
  blog_posts.value = await resp.json()
}

fetchPosts()


</script>

<template>
    <h2>Blog</h2>
    <p>Some content</p>
    <UPageGrid>
      <UCard variant="subtle" class="w-full" v-for="post in blog_posts" :key="post.title">
        <template #header>
          <h3 class="font-semibold">{{ post.title }}</h3>
        </template>

        {{ post.body }}
      </UCard>
    </UPageGrid>
</template>

<style>

</style>

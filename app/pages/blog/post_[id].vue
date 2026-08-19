<script setup lang="ts">

const route = useRoute()

const { data: blog_post, error } = await useFetch(() => `https://jsonplaceholder.typicode.com/posts/${route.params.id}`)

const { data: comments } = await useFetch("https://jsonplaceholder.typicode.com/comments", {
  query: { 
    postId: route.params.id }
})
</script>

<template>
  <h2 class="text-2xl font-semibold tracking-tight">Blog post</h2>
  <UCard variant="subtle" class="w-full" v-if="blog_post">
    <template #header>
      <h3 class="font-semibold">{{ blog_post.title }}</h3>
    </template>
    <p>{{ blog_post.body }}</p>
  </UCard>
  <p v-else="blog_post">Blog post with ID {{ route.params.id }} not found.</p>
  <br>
  <h2 class="text-2xl font-semibold tracking-tight">Comments</h2>
  <UPageList v-if="comments">
    <UPageCard v-for="comment in comments" :key="comment.id"
      :title="comment.name"
      :description="comment.body">
      <template #footer>
        <UUser :name="comment.email" avatar="{ alt: comment.email }"/>
      </template>
    </UPageCard>
  </UPageList>
  <p v-else="comment">No comments.</p>

</template>

<style>

</style>

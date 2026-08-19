<script setup lang="ts">
const { data: blog_posts } = await useFetch("https://jsonplaceholder.typicode.com/posts")

const page = ref(1)
</script>

<template>
  <div>
    <h2 class="text-2xl font-semibold tracking-tight"></h2>
    <p>These are all the blog posts</p>
    <br>
    <UPageGrid>
      <UPageCard variant="subtle" class="w-full" 
        v-for="post in blog_posts" 
        :key="post.id" 
        :title="post.title"
        :description="post.body"
        :to="`/blog/post_${post.id}`"
      />
    </UPageGrid>
    <UPagination v-model:page="page" :items-per-page="20" :total="100" />
  </div>
</template>

<style>

</style>

<script setup lang="ts">
interface Post {
  id: number
  title: string
  body: string
}
const { data: blog_posts } = await useFetch<Post[]>(
  'https://jsonplaceholder.typicode.com/posts'
)

const page = ref(1)
</script>

<template>
  <div>
    <p>These are all the blog posts</p>
    <br>
    <UPageGrid>
      <UPageCard
        v-for="post in blog_posts"
        variant="subtle"
        :key="post.id"
        class="w-full"
        :title="post.title"
        :description="post.body"
        :to="`/blog/post_${post.id}`"
      />
    </UPageGrid>
    <UPagination
      v-model:page="page"
      :items-per-page="20"
      :total="100"
    />
  </div>
</template>

<style>

</style>

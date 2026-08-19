<script setup lang="ts">
interface Post {
  id: number
  title: string
  body: string
}

const page = ref(1)
const limit = 12

const { data: blog_posts } = await useFetch<Post[]>(
  'https://jsonplaceholder.typicode.com/posts', {
    query: {
        _page: page,
        _limit: limit
      }
  }
)
</script>

<template>
  <div>
    <p>These are all the blog posts.</p>
    <br>
    <UPageGrid>
      <UPageCard
        v-for="post in blog_posts"
        :key="post.id"
        variant="subtle"
        class="w-full"
        :title="post.title"
        :description="post.body"
        :to="`/blog/post_${post.id}`"
      />
    </UPageGrid>
    <br>
    <UPagination
      v-model:page="page"
      :items-per-page="limit"
      :total="100"
    />
  </div>
</template>

<style>

</style>

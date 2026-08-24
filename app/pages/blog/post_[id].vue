<script setup lang="ts">
const route = useRoute()

interface Post {
  userId: number
  id: number
  title: string
  body: string
}

interface Comment {
  id: number
  name: string
  body: string
  email: string
}

interface User {
  id: number
  name: string
  username: string
  email: string
  company: {
    name: string
    catchPhrase: string
    bs: string
  }
}

const { data: blog_post } = await useFetch<Post>(
  () => `https://jsonplaceholder.typicode.com/posts/${route.params.id}`
)

const { data: user } = await useFetch<User>(
  `https://jsonplaceholder.typicode.com/users/${blog_post.value?.userId}`
)

const { data: comments } = await useFetch<Comment[]>(
  'https://jsonplaceholder.typicode.com/comments',
  {
    query: {
      postId: route.params.id }
  }
)
</script>

<template>
  <div>
    <h2 class="text-2xl font-semibold tracking-tight">
      Blog post
    </h2>
    <UCard
      v-if="blog_post"
      variant="subtle"
      class="w-full"
    >
      <template #header>
        <h3 class="font-semibold">
          {{ blog_post.title }}
        </h3>
      </template>
      <p>
        {{ blog_post.body }}
      </p>
      <template #footer>
        <UUser
          v-if="user"
          :name="user.name"
          :description="user.company.name"
          :avatar="{ alt: user.name }"
          :to="`/users/user_${user.id}`"
        />
      </template>
    </UCard>
    <p v-else>
      Blog post with ID {{ route.params.id }} not found.
    </p>
    <br>
    <h2 class="text-2xl font-semibold tracking-tight">
      Comments
    </h2>
    <UPageList
      v-if="comments"
    >
      <UPageCard
        v-for="comment in comments"
        :key="comment.id"
        :title="comment.name"
        :description="comment.body"
      >
        <template #footer>
          <UUser
            :name="comment.email"
            :avatar="{ alt: comment.email }"
          />
        </template>
      </UPageCard>
    </UPageList>
    <p v-else>
      No comments.
    </p>
  </div>
</template>

<style>

</style>

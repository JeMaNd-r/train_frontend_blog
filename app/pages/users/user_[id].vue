<script setup lang="ts">
const route = useRoute()

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

interface Post {
  id: number
  title: string
  body: string
}

const { data: user } = await useFetch<User>(
  () => `https://jsonplaceholder.typicode.com/users/${route.params.id}`
)

const page = ref(1)
const limit = 5

const { data: posts } = await useFetch<Post[]>(
  'https://jsonplaceholder.typicode.com/posts',
  {
    query: {
      userId: route.params.id,
      _page: page,
      _limit: limit
    }
  }
)

const { data: allPosts } = await useFetch<Post[]>(
  'https://jsonplaceholder.typicode.com/posts',
  {
    query: {
      userId: route.params.id
    }
  }
)
const totalPosts = computed(() => allPosts.value?.length ?? 0)
</script>

<template>
  <div>
    <h2 class="text-2xl font-semibold tracking-tight">
      {{ user?.name }}
    </h2>
    <UCard
      v-if="user"
      variant="subtle"
      class="w-full"
    >
      <template #header>
        <h3 class="font-semibold">
          Username: {{ user.username }}
        </h3>
      </template>
      <p>
        Company: {{ user.company.name }}
      </p>
      <p>
        "{{ user.company.catchPhrase }}"
      </p>
    </UCard>
    <p v-else>
      User with ID {{ route.params.id }} not found.
    </p>
    <br>
    <h2 class="text-2xl font-semibold tracking-tight">
      Posts
    </h2>
    <UPageList
      v-if="posts"
    >
      <UPageCard
        v-for="post in posts"
        :key="post.id"
        :title="post.title"
        :description="post.body"
        :to="`/blog/post_${post.id}`"
      />
    </UPageList>
    <p v-else>
      No posts made by that user.
    </p>
    <br>
    <UPagination
      v-model:page="page"
      :items-per-page="limit"
      :total="totalPosts"
    />
  </div>
</template>

<style>

</style>

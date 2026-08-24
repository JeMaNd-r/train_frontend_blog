<script setup lang="ts">
interface User {
  id: number
  name: string
  email: string
}

const { data: users } = await useFetch<User[]>(
  'https://jsonplaceholder.typicode.com/users'
)
</script>

<template>
  <div>
    <h2 class="text-2xl font-semibold tracking-tight">
      Users
    </h2>
    <p>These are the people commenting and posting in this blog.</p>
    <br>
    <UPageGrid>
      <UUser
        v-for="user in users"
        :key="user.id"
        variant="subtle"
        class="w-full"
        :name="user.name"
        :description="user.email"
        :to="`/users/user_${user.id}`"
        :avatar="{ alt: user.name }"
      />
    </UPageGrid>
  </div>
</template>

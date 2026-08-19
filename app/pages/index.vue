<script setup lang="ts">
const pages = ref([
  {
    title: "Blog",
    description: "Blog posts",
    icon: "i-lucide-book-open",
    to: "/blog"
  }
])
</script>

<template>
  <div>
    <h2 class="text-2xl font-semibold tracking-tight">Welcome!</h2>
    <p>Welcome to this cool travel blog.</p>
    <br>
    <p>You can see the posts under the Blog link. And you can always go back to this Index.</p>
    <br>

    <UPageGrid>
      <UPageCard v-for="(page, index) in pages" :key="index", v-bind="page" />
    </UPageGrid>
  </div>
</template>

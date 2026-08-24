<script setup lang="ts">
const features = ref([
  {
    title: 'Blog posts',
    description: 'View posts in PageGrid and individually',
    icon: 'i-lucide-book-open',
    url: '/blog'
  },
  {
    title: 'Comments',
    description: 'View comments to individual post',
    icon: 'i-lucide-message-circle',
    url: '/blog/post_1'
  },
  {
    title: 'Users',
    description: 'View authors of posts',
    icon: 'i-lucide-users',
    url: '/users'
  }
])

interface Commit {
  commit: {
    message: string
    author: {
      name: string
      date: string
    }
  }
  html_url: string
}

const page = ref(1)
const limit = 5

const { data: commits } = await useFetch<Commit[]>(
  'https://api.github.com/repos/JeMaNd-r/train_frontend_blog/commits',
  {
    query: {
      page,
      per_page: limit
    }
  }
)

const commitsTimeline = computed(() =>
  (commits.value ?? []).map(commit => ({
    title: commit.commit.message,
    date: new Date(commit.commit.author.date).toLocaleString('en-GB', {
      day: 'numeric',
      month: 'short',
      year: 'numeric',
      hour: 'numeric',
      minute: '2-digit'
    }),
    description: commit.commit.author.name,
    icon: 'i-lucide-code'
  }))
)

const { data: allCommits } = await useFetch<Commit[]>(
  'https://api.github.com/repos/JeMaNd-r/train_frontend_blog/commits'
)
const totalCommits = computed(() => allCommits.value?.length ?? 0)
</script>

<template>
  <div>
    <h2 class="text-2xl font-semibold tracking-tight">
      About this blog
    </h2>
    <p>
      Project to learn frontend with Nuxt and Vue, as well as NuxtUI and JSONPlaceholder as test API.
    </p>
    <br>
    <UPageCard
      title="What's its purpose?"
      icon="i-lucide-goal"
      description="The goal was to set up a travel blog that requests data from the JSONPlaceholder API and nicely presents the content using NuxtUI."
    />
    <br>

    <h2 class="text-2xl font-semibold tracking-tight">
      Features
    </h2>
    <UPageGrid>
      <UPageFeature
        v-for="feature in features"
        :key="feature.title"
        :title="feature.title"
        :description="feature.description"
        :icon="feature.icon"
        :to="feature.url"
        target="_blank"
      />
    </UPageGrid>
    <br>

    <h2 class="text-2xl font-semibold tracking-tight">
      Commit history
    </h2>
    <UTimeline
      v-if="commitsTimeline"
      :items="commitsTimeline"
    />
    <p v-else>
      No commits made.
    </p>
    <UPagination
      v-model:page="page"
      :items-per-page="limit"
      :total="totalCommits"
    />
  </div>
</template>

<script setup lang="ts">
import type { NavigationMenuItem } from '@nuxt/ui'

useHead({
  meta: [
    { name: 'viewport', content: 'width=device-width, initial-scale=1' }
  ],
  link: [
    { rel: 'icon', href: '/favicon.ico' }
  ],
  htmlAttrs: {
    lang: 'en'
  }
})

const title = 'Cool travel blog'
const description = 'A training project to learn functionalities of Nuxt and NuxtUI as well as connecting to simple API.'

useSeoMeta({
  title,
  description,
  ogTitle: title,
  ogDescription: description,
  ogImage: 'https://ui.nuxt.com/assets/templates/nuxt/starter-light.png',
  twitterCard: 'summary_large_image'
})

const nav_items = ref<NavigationMenuItem[]>([
  {
    label: 'Home',
    icon: 'i-lucide-house',
    to: '/'
  },
  {
    label: 'Blog',
    icon: 'i-lucide-book-open',
    to: '/blog',
    children: [
      {
        label: 'All posts',
        icon: 'i-lucide-book-open',
        to: '/blog'
      },
      {
        label: 'First post',
        icon: 'i-lucide-file-text',
        to: '/blog/post_1'
      }
    ]
  },
  {
    label: 'About',
    icon: 'i-lucide-info',
    to: '/about'
  }
])
</script>

<template>
  <UApp>
    <UHeader>
      <template #left>
        <NuxtLink to="/">
          <AppLogo class="w-auto h-6 shrink-0" />
        </NuxtLink>
        <p> - Cool Travel Blog</p>
      </template>

      <template #right>
        <UColorModeButton />

        <UButton
          to="https://github.com/JeMaNd-r/train_frontend_blog"
          target="_blank"
          icon="i-simple-icons-github"
          aria-label="GitHub"
          color="neutral"
          variant="ghost"
        />
      </template>
    </UHeader>

    <UContainer>
      <UNavigationMenu :items="nav_items" />

      <UMain>
        <NuxtPage />
      </UMain>
    </UContainer>

    <USeparator icon="i-simple-icons-nuxtdotjs" />

    <UFooter>
      <FooterColumn />
    </UFooter>
  </UApp>
</template>

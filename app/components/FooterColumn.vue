<script setup lang="ts">
import type { FooterColumn } from '@nuxt/ui'

const columns: FooterColumn[] = [
  {
    label: 'App',
    children: [
      {
        label: 'Index',
        to: '/'
      },
      {
        label: 'About',
        to: '/about'
      }
    ]
  },
  {
    label: 'Blog',
    children: [
      {
        label: 'Posts',
        to: '/blog'
      },
      {
        label: 'Example post',
        to: '/blog/post_1'
      }
    ]
  },
  {
    label: 'People',
    children: [
      {
        label: 'Users',
        to: '/users'
      },
      {
        label: 'Example user',
        to: '/users/user_1'
      }
    ]
  }
]
</script>

<template>
  <UFooterColumns :columns="columns">
    <template #right>
      <p class="text-sm text-muted">
        Built with Nuxt UI • © JeMaNd-r, {{ new Date().getFullYear() }}
      </p>
    </template>
  </UFooterColumns>
</template>

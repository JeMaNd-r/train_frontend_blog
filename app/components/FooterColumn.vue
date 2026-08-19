<script setup lang="ts">
import type { FooterColumn } from '@nuxt/ui'

const columns: FooterColumn[] = [
  {
    label: 'About',
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
      },
      {
        label: 'Photos',
        to: '/blog'
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

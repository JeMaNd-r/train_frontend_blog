<script setup lang="ts">
import type { FooterColumn } from '@nuxt/ui'

const columns: FooterColumn[] = [
  {
    label: 'About',
    children: [
      {
        label: 'Index',
        to: '/',
        target: '_blank'
      },
      {
        label: 'About',
        to: '/',
        target: '_blank'
      }
    ]
  },
  {
    label: 'Blog',
    children: [
      {
        label: 'Posts',
        to: '/blog',
        target: '_blank'
      },
      {
        label: 'Comments',
        to: '/blog',
        target: '_blank'
      },
      {
        label: 'Photos',
        to: '/blog',
        target: '_blank'
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

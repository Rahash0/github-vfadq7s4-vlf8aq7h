<script setup lang="ts">
defineProps<{
  articles: Array<{
    title?: string
    subtitle?: string
    slug?: string | { current?: string }
    heroImage?: string
    category?: {
      title?: string
      slug?: string | { current?: string }
    }
  }>
}>()

const normalizeSlug = (value?: string | { current?: string }) =>
  typeof value === 'string' ? value : value?.current || ''
</script>

<template>
  <section>
    <h2 class="text-2xl font-semibold text-highlighted">Continue exploring</h2>
    <div class="mt-6 grid gap-4 md:grid-cols-3">
      <NuxtLink
        v-for="article in articles"
        :key="normalizeSlug(article.slug) || article.title || 'No title'"
        :to="`/blog/${normalizeSlug(article.category?.slug)}/${normalizeSlug(article.slug)}`"
        class="block border border-[#E5E8ED] bg-[#FFFFFF] p-4 hover:bg-[#F7F5F2]"
      >
        <img
          v-if="article.heroImage"
          :src="article.heroImage"
          :alt="article.title || 'No title'"
          class="mb-4 aspect-[16/9] w-full object-cover"
        >
        <div
          v-else
          class="mb-4 aspect-[16/9] w-full"
        >
          <AppImagePlaceholder label="Beyongo guide" tone="secondary" />
        </div>
        <UBadge
          v-if="article.category?.title"
          color="neutral"
          variant="subtle"
          class="mb-3 bg-[#E8EEF6] text-[#0A2540] ring-[#E5E8ED]"
        >
          {{ article.category.title }}
        </UBadge>
        <h3 class="font-semibold text-highlighted">{{ article.title || 'No title' }}</h3>
        <p class="mt-2 text-sm text-muted">{{ article.subtitle || 'No subtitle' }}</p>
      </NuxtLink>
    </div>
  </section>
</template>

<script setup lang="ts">
defineProps<{
  article: {
    title: string
    subtitle: string
    slug: string
    image: string
    category: {
      title: string
      slug: string
    }
    tag?: string
    readTime?: number
    publishedAt?: string
  }
}>()

const imageFailed = ref(false)
</script>

<template>
  <NuxtLink
    :to="`/blog/${article.category.slug}/${article.slug}`"
    class="group block bg-[#FFFFFF]"
  >
    <img
      v-if="article.image && !imageFailed"
      :src="article.image"
      :alt="article.title"
      class="aspect-[16/9] w-full rounded-lg object-cover"
      @error="imageFailed = true"
    >
    <div
      v-else
      class="aspect-[16/9] w-full"
    >
      <AppImagePlaceholder
        label="Beyongo guide"
        :title="article.category.title"
        tone="secondary"
      />
    </div>
    <div class="pb-6 pt-4">
      <AppBlogBadge :label="article.tag || article.category.title" />
      <h3 class="mt-2 text-base font-bold leading-snug text-highlighted group-hover:text-[#D84F2A]">
        {{ article.title }}
      </h3>
      <div class="mt-3 flex flex-wrap items-center gap-3">
        <span v-if="article.publishedAt" class="text-xs font-medium leading-4 text-[#6B7380]">
          {{ article.publishedAt }}
        </span>
        <span
          v-if="article.publishedAt && article.readTime"
          class="h-1 w-1 rounded-full bg-[#E5E8ED]"
        />
        <span v-if="article.readTime" class="text-xs font-medium leading-4 text-[#6B7380]">
          {{ article.readTime }} min read
        </span>
      </div>
    </div>
  </NuxtLink>
</template>

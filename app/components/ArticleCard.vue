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
    readTime?: number
  }
}>()

const imageFailed = ref(false)
</script>

<template>
  <NuxtLink
    :to="`/blog/${article.category.slug}/${article.slug}`"
    class="group block border border-[#E5E8ED] bg-[#FFFFFF] hover:bg-[#F7F5F2]"
  >
    <img
      v-if="article.image && !imageFailed"
      :src="article.image"
      :alt="article.title"
      class="aspect-[4/3] w-full object-cover md:aspect-[16/10]"
      @error="imageFailed = true"
    >
    <div
      v-else
      class="aspect-[4/3] w-full md:aspect-[16/10]"
    >
      <AppImagePlaceholder
        label="Beyongo guide"
        :title="article.category.title"
        tone="secondary"
      />
    </div>
    <div class="p-4">
      <div class="flex flex-wrap items-center gap-3">
        <UBadge
          color="neutral"
          variant="subtle"
          class="bg-[#E8EEF6] text-[#0A2540] ring-[#E5E8ED]"
        >
          {{ article.category.title }}
        </UBadge>
        <span v-if="article.readTime" class="text-xs text-muted">
          {{ article.readTime }} min read
        </span>
      </div>
      <h3 class="mt-3 text-lg font-semibold text-highlighted group-hover:text-[#D84F2A]">
        {{ article.title }}
      </h3>
      <p class="mt-2 text-sm leading-6 text-muted">
        {{ article.subtitle }}
      </p>
    </div>
  </NuxtLink>
</template>

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
    readTime: number
    publishedAt: string
  }
}>()

const imageFailed = ref(false)
</script>

<template>
  <section class="grid gap-7 lg:grid-cols-[55fr_45fr] lg:items-center">
    <div class="order-1">
      <AppBlogBadge label="Featured guide" />
      <h2 class="mt-4 max-w-xl text-3xl font-bold leading-tight text-highlighted lg:text-5xl">
        {{ article.title }}
      </h2>
      <p class="mt-4 max-w-xl text-sm leading-6 text-muted md:text-base md:leading-7">
        {{ article.subtitle }}
      </p>
      <div class="mt-5 flex flex-wrap items-center gap-3 text-sm font-normal leading-5 text-[#6B7380]">
        <span>{{ article.readTime }} min read</span>
        <span class="h-1 w-1 rounded-full bg-[#E5E8ED]" />
        <span>{{ article.publishedAt }}</span>
      </div>
      <UButton
        class="mt-6"
        label="Read guide"
        :to="`/blog/${article.category.slug}/${article.slug}`"
        color="primary"
        :ui="{ base: 'flex w-fit items-center gap-2 rounded-lg bg-[#D84F2A] px-6 py-2 text-white hover:bg-[#BE4423] active:bg-[#BE4423] focus-visible:outline-[#D84F2A]' }"
      />
    </div>

    <NuxtLink
      :to="`/blog/${article.category.slug}/${article.slug}`"
      class="order-2 block"
    >
      <img
        v-if="article.image && !imageFailed"
        :src="article.image"
        :alt="article.title"
        class="aspect-[16/9] w-full rounded-xl object-cover lg:aspect-[16/10]"
        @error="imageFailed = true"
      >
      <div
        v-else
        class="aspect-[16/9] w-full lg:aspect-[16/10]"
      >
        <AppImagePlaceholder
          label="Featured guide"
          :title="article.category.title"
          tone="primary"
          class="rounded-xl p-6"
        />
      </div>
    </NuxtLink>
  </section>
</template>

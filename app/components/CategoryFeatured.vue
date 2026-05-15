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
  <section class="grid gap-6 border-y border-muted py-8 lg:grid-cols-[55fr_45fr] lg:items-center">
    <div class="order-2 lg:order-1">
      <UBadge
        color="neutral"
        variant="subtle"
        class="bg-[#FBEDE8] text-[#D84F2A] ring-[#FBEDE8]"
      >
        Featured guide
      </UBadge>
      <h2 class="mt-4 text-3xl font-semibold text-highlighted lg:text-4xl">
        {{ article.title }}
      </h2>
      <p class="mt-4 text-base leading-7 text-muted">
        {{ article.subtitle }}
      </p>
      <div class="mt-4 flex flex-wrap gap-3 text-sm text-muted">
        <span>{{ article.publishedAt }}</span>
        <span>{{ article.readTime }} min read</span>
      </div>
      <UButton
        class="mt-6"
        label="Read guide"
        :to="`/blog/${article.category.slug}/${article.slug}`"
        color="primary"
        :ui="{ base: 'bg-[#D84F2A] hover:bg-[#BE4423] active:bg-[#BE4423] text-white focus-visible:outline-[#D84F2A]' }"
      />
    </div>

    <NuxtLink
      :to="`/blog/${article.category.slug}/${article.slug}`"
      class="order-1 block lg:order-2"
    >
      <img
        v-if="article.image && !imageFailed"
        :src="article.image"
        :alt="article.title"
        class="aspect-[4/3] w-full object-cover lg:aspect-[16/12]"
        @error="imageFailed = true"
      >
      <div
        v-else
        class="aspect-[4/3] w-full lg:aspect-[16/12]"
      >
        <AppImagePlaceholder
          label="Featured guide"
          :title="article.category.title"
          tone="primary"
          class="p-6"
        />
      </div>
    </NuxtLink>
  </section>
</template>

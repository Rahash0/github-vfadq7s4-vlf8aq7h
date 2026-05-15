<script setup lang="ts">
defineProps<{
  title: string
  subtitle: string
  author: {
    name: string
    avatar: string
  }
  publishedAt: string
  readTime: string | number
  heroImage: string
  metaTopic: string
  metaKeyWay: string
  metaBestFor: string
}>()

const imageFailed = ref(false)
</script>

<template>
  <section class="space-y-6">
    <div>
      <h1 class="text-4xl font-semibold tracking-normal text-highlighted lg:text-6xl">
        {{ title }}
      </h1>
      <p class="mt-4 text-lg leading-8 text-muted">
        {{ subtitle }}
      </p>
    </div>

    <div class="flex flex-wrap items-center gap-3 text-sm text-muted">
      <UAvatar
        :src="author.avatar"
        :alt="author.name"
        size="sm"
        class="bg-[#E8EEF6] text-[#6B7380]"
      />
      <span class="font-medium text-highlighted">{{ author.name }}</span>
      <span>{{ publishedAt }}</span>
      <span>{{ readTime }} min read</span>
    </div>

    <img
      v-if="heroImage && !imageFailed"
      :src="heroImage"
      :alt="title"
      class="aspect-[16/6] w-full object-cover"
      @error="imageFailed = true"
    >
    <div
      v-else
      class="aspect-[16/6] w-full"
    >
      <AppImagePlaceholder
        label="Beyongo article"
        :title="metaTopic"
        tone="accent"
        class="p-6"
      />
    </div>

    <dl class="grid grid-cols-2 gap-4 border-y border-muted py-5 lg:grid-cols-4">
      <div>
        <dt class="text-xs font-medium uppercase tracking-[1px] text-dimmed">Topic</dt>
        <dd class="mt-1 text-sm font-medium text-highlighted">{{ metaTopic }}</dd>
      </div>
      <div>
        <dt class="text-xs font-medium uppercase tracking-[1px] text-dimmed">Reading time</dt>
        <dd class="mt-1 text-sm font-medium text-highlighted">{{ readTime }} min read</dd>
      </div>
      <div>
        <dt class="text-xs font-medium uppercase tracking-[1px] text-dimmed">Key way</dt>
        <dd class="mt-1 text-sm font-medium text-highlighted">{{ metaKeyWay }}</dd>
      </div>
      <div>
        <dt class="text-xs font-medium uppercase tracking-[1px] text-dimmed">Best for</dt>
        <dd class="mt-1 text-sm font-medium text-highlighted">{{ metaBestFor }}</dd>
      </div>
    </dl>
  </section>
</template>

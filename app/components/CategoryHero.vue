<script setup lang="ts">
defineProps<{
  title: string
  description: string
}>()
</script>

<template>
  <section class="py-8 md:py-9">
    <p class="text-xs font-medium uppercase tracking-[1px] text-dimmed">Beyongo guides</p>
    <h1 class="mt-3 text-4xl font-bold tracking-normal text-highlighted lg:text-6xl">
      {{ title }}
    </h1>
    <p class="mt-4 max-w-3xl text-base leading-7 text-muted md:text-lg md:leading-8">
      {{ description }}
    </p>
  </section>
</template>

<script setup lang="ts">
defineProps<{
  title: string
  description: string
}>()
</script>

<template>
  <section class="py-10">
    <p class="font-mono text-xs uppercase text-dimmed">Beyongo guides</p>
    <h1 class="mt-3 text-4xl font-semibold tracking-normal text-highlighted lg:text-6xl">
      {{ title }}
    </h1>
    <p class="mt-4 max-w-3xl text-lg leading-8 text-muted">
      {{ description }}
    </p>
  </section>
</template>

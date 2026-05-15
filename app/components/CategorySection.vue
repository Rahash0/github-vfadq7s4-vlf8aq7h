<script setup lang="ts">
defineProps<{
  title: string
}>()
</script>

<template>
  <section class="py-8 md:py-9">
    <h2 class="text-xl font-bold text-highlighted md:text-2xl">
      {{ title }}
    </h2>
    <div class="mt-5">
      <slot />
    </div>
  </section>
</template>

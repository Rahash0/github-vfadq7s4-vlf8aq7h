<script setup lang="ts">
defineProps<{
  title: string
}>()
</script>

<template>
  <section class="py-10">
    <h2 class="text-2xl font-semibold text-highlighted">
      {{ title }}
    </h2>
    <div class="mt-6">
      <slot />
    </div>
  </section>
</template>

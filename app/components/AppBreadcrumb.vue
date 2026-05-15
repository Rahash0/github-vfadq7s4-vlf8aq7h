<script setup lang="ts">
defineProps<{
  items: Array<{
    label: string
    to?: string
  }>
}>()
</script>

<template>
  <UBreadcrumb :items="items" />
</template>

<script setup lang="ts">
defineProps<{
  total: number
  itemsPerPage: number
}>()

const page = defineModel<number>('page', { default: 1 })
</script>

<template>
  <div class="flex justify-center border-t border-muted pt-8">
    <UPagination
      v-model:page="page"
      :total="total"
      :items-per-page="itemsPerPage"
    />
  </div>
</template>
